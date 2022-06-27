<template>
  <div class="containerRegisterNewQuestion">
    <form @submit="addNewQuestion($event)">
      <h1>Registrar questão</h1>

      <label>Digite a questão *</label>
      <input type="text" placeholder="Qual o maior...?" v-model="question" />

      <label>Preencha as alternativas *</label>
      <div class="inputAlternative">
        <input
          type="text"
          placeholder="Alternativa A"
          v-model="alternatives[0].answer"
        />
        <button type="button" @click="() => changeCorrectAnswer('A')" :class="{answerSelected: selectCorrectAnswer === 'A'}">
          <i
            class="bx bx-check"
            v-if="selectCorrectAnswer === 'A'"
          ></i>
					<p v-else>A</p>
        </button>
      </div>
      <div class="inputAlternative">
        <input
          type="text"
          placeholder="Alternativa B"
          v-model="alternatives[1].answer"
        />
        <button type="button" @click="() => changeCorrectAnswer('B')" :class="{answerSelected: selectCorrectAnswer === 'B'}">
          <i
            class="bx bx-check"
            v-if="selectCorrectAnswer === 'B'"
          ></i>
					<p v-else>B</p>
        </button>
      </div>
      <div class="inputAlternative">
        <input
          type="text"
          placeholder="Alternativa C"
          v-model="alternatives[2].answer"
        />
        <button type="button" @click="() => changeCorrectAnswer('C')" :class="{answerSelected: selectCorrectAnswer === 'C'}">
          <i
            class="bx bx-check"
            v-if="selectCorrectAnswer === 'C'"
          ></i>
					<p v-else>C</p>
        </button>
      </div>
      <div class="inputAlternative">
        <input
          type="text"
          placeholder="Alternativa D"
          v-model="alternatives[3].answer"
        />
        <button type="button" @click="() => changeCorrectAnswer('D')" :class="{answerSelected: selectCorrectAnswer === 'D'}">
          <i
            class="bx bx-check"
            v-if="selectCorrectAnswer === 'D'"
          ></i>
					<p v-else>D</p>
        </button>
      </div>

      <label>URL da imagem</label>
      <input type="url" placeholder="Digite a URL de uma imagem" />

      <label for="selectDifficulty">Selecione a dificuldade da questão *</label>
      <select name="selectDifficulty" v-model="selectDifficulty">
        <option value="easy">Fácil</option>
        <option value="medium">Médio</option>
        <option value="hard">Difícil</option>
      </select>
      <label for="selectTheme">Selecione o tema da pergunta *</label>
      <select name="selectTheme" v-model="selectTheme">
        <option value="history">História</option>
        <option value="math">Matemática</option>
        <option value="programation">Programação</option>
        <option value="geography">Geografia</option>
        <option value="movie">Cinema</option>
        <option value="science">Ciência</option>
        <option value="sports">Esportes</option>
        <option value="english">Inglês</option>
      </select>
      <div class="buttonsModal">
        <button type="submit">Registrar</button>
        <button type="button" @click="$emit('setModal')">Cancelar</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";

const Toast = Swal.mixin({
  toast: true,
  position: 'top-end',
  showConfirmButton: false,
  timer: 3000,
  timerProgressBar: true,
  didOpen: (toast) => {
    toast.addEventListener('mouseenter', Swal.stopTimer)
    toast.addEventListener('mouseleave', Swal.resumeTimer)
  }
})

export default {
  name: "Modal",
  data() {
    return {
      question: "",
      alternatives: [
        {
          alternative: "A",
          answer: "",
        },
        {
          alternative: "B",
          answer: "",
        },
        {
          alternative: "C",
          answer: "",
        },
        {
          alternative: "D",
          answer: "",
        },
      ],
      selectTheme: "",
      selectCorrectAnswer: "",
      selectDifficulty: "",
    };
  },
  methods: {
    async addNewQuestion(e) {
      e.preventDefault();

      let questionObject = {
        question: this.question,
        alternatives: this.alternatives,
        correctAnswer: this.selectCorrectAnswer,
        difficulty: this.selectDifficulty,
        theme: this.selectTheme,
      };

      const data = await axios
        .post("https://quiz-api-jgsl.herokuapp.com/questions", questionObject)
        .then( () => {
          this.question = "";
          this.alternatives = [
            {
              alternative: "A",
              answer: "",
            },
            {
              alternative: "B",
              answer: "",
            },
            {
              alternative: "C",
              answer: "",
            },
            {
              alternative: "D",
              answer: "",
            },
          ];
          this.selectTheme = "";
          this.selectCorrectAnswer = "";
          this.selectDifficulty = "";
					Toast.fire({
						icon: 'success',
						title: 'Questão adicionada com sucesso.'
					})
        });

      this.$emit("reloadTable");
    },
    changeCorrectAnswer(correctAnswer) {
      this.selectCorrectAnswer = correctAnswer;
    },
  },
  components: {},
  emits: ["setModal", "reloadTable"],
};
</script>

<style lang="sass" src="./style.scss" scoped></style>
