<template>
  <div class="containerTable">
    <header>
      <h1>Banco de questões</h1>
      <button @click="() => (isModal = true)">
        <i class="bx bx-plus"></i> Nova questão
      </button>
    </header>

    <div class="table">
      <div class="titlesTable">
        <span class="spanQuestion">Questão</span>
        <span>Resposta</span>
        <span>Dificuldade</span>
        <span>Tema</span>
        <span class="actions">Ações</span>
      </div>
      <div
        class="flexContentTable"
        v-for="question in arrayQuestions"
        :key="question.id"
      >
        <div class="contentTable">
          <span data-label="Questão" class="spanQuestion">{{
            question.question
          }}</span>
          <span data-label="Resposta">{{ question.correctAnswer }}</span>
          <span data-label="Dificuldade">{{ question.difficulty }}</span>
          <span data-label="Tema">{{ question.theme }}</span>
          <span class="actions" data-label="Ações">
            <button @click="() => toggleEditModal(question)">
              <i
                class="bx bxs-edit-alt"
                style="color: #f7f8fc; font-size: 1.3rem"
              ></i>
            </button>
            <button @click="() => deleteQuestion(question.id)">
              <i
                class="bx bxs-trash"
                style="color: #f7f8fc; font-size: 1.3rem"
              ></i>
            </button>
          </span>
        </div>
      </div>
    </div>
  </div>

  <Modal @reloadTable="loadApi" v-show="isModal" @setModal="setModalFalse" />
  <EditModal
    @reloadTable="loadApi"
    v-show="isEditModal"
    @setModal="setModalFalse"
		:questionToEdit="questionToEdit"
		:answerA="answerA"  
		:answerB="answerB"
		:answerC="answerC"
		:answerD="answerD"
  />
</template>

<script>
import axios from "axios";

import Modal from "../Modal/modal.vue";
import EditModal from "../EditModal/editmodal.vue";

const Toast = Swal.mixin({
  toast: true,
  position: "top-end",
  showConfirmButton: false,
  timer: 3000,
  timerProgressBar: true,
  didOpen: (toast) => {
    toast.addEventListener("mouseenter", Swal.stopTimer);
    toast.addEventListener("mouseleave", Swal.resumeTimer);
  },
});

export default {
  name: "Table",
  data() {
    return {
      isModal: false,
      isEditModal: false,
      idEditModal: "",

			answerA: "",
			answerB: "",
			answerC: "",
			answerD: "",

      arrayQuestions: [],

      questionToEdit: {},
    };
  },
  methods: {
    toggleEditModal(question) {
			this.answerA = question.alternatives[0].answer
			this.answerB = question.alternatives[1].answer
			this.answerC = question.alternatives[2].answer
			this.answerD = question.alternatives[3].answer
			this.questionToEdit = question;
      this.isEditModal = true;
    },
    setModalFalse() {
      this.isModal = false;
      this.isEditModal = false;
    },
    async loadApi() {
      const data = await axios.get(
        "https://quiz-api-jgsl.herokuapp.com/questions"
      );
      this.arrayQuestions = data.data;
      this.$emit("reloadAdmin");
    },
    async deleteQuestion(id) {
      Swal.fire({
        title: "Você tem certeza?",
        text: "Deseja deletar essa questão?",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3751FF",
        cancelButtonColor: "#d33",
        confirmButtonText: "Sim, deletar questão!",
      }).then(async (result) => {
        if (result.isConfirmed) {
          await axios
            .delete(`https://quiz-api-jgsl.herokuapp.com/questions/${id}`)
            .then(() => {
              this.loadApi();
              this.$emit("reloadAdmin");
              Toast.fire({
                icon: "success",
                title: "Questão deletada com sucesso.",
              });
            });
        }
      });
    },
  },
  mounted() {
    this.loadApi();
  },
  components: {
    Modal,
    EditModal,
  },
  emits: ["reloadAdmin"],
};
</script>

<style lang="sass" src="./style.scss" scoped></style>
