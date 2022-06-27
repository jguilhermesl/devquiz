<template>
  <div class="containerRegisterNewQuestion">
    <form @submit="editQuestion($event)">
      <h1>Editar questão</h1>

      <label>Digite a questão *</label>
      <input type="text" placeholder="Qual o maior...?" v-model="questionToEdit.question" />

      <label>Preencha as alternativas *</label>
      <div class="inputAlternative">
        <input type="text" placeholder="Alternativa A" v-model="answerA"/>
				<button type="button" @click="() => changeCorrectAnswer('A')" :class="{answerSelected: questionToEdit.correctAnswer === 'A'}">
          <i
            class="bx bx-check"
            v-if="questionToEdit.correctAnswer === 'A'"
          ></i>
					<p v-else>A</p>
        </button>
      </div>
      <div class="inputAlternative">
        <input type="text" placeholder="Alternativa B" v-model="answerB"/>
        <button type="button" @click="() => changeCorrectAnswer('B')" :class="{answerSelected: questionToEdit.correctAnswer === 'B'}">
          <i
            class="bx bx-check"
            v-if="questionToEdit.correctAnswer === 'B'"
          ></i>
					<p v-else>B</p>
        </button>
      </div>
      <div class="inputAlternative">
        <input type="text" placeholder="Alternativa C" v-model="answerC"/>
        <button type="button" @click="() => changeCorrectAnswer('C')" :class="{answerSelected: questionToEdit.correctAnswer === 'C'}">
          <i
            class="bx bx-check"
            v-if="questionToEdit.correctAnswer === 'C'"
          ></i>
					<p v-else>C</p>
        </button>
      </div>
      <div class="inputAlternative">
        <input type="text" placeholder="Alternativa D" v-model="answerD"/>
        <button type="button" @click="() => changeCorrectAnswer('D')" :class="{answerSelected: questionToEdit.correctAnswer === 'D'}">
          <i
            class="bx bx-check"
            v-if="questionToEdit.correctAnswer === 'D'"
          ></i>
					<p v-else>D</p>
        </button>
      </div>

      <label>URL da imagem</label>
      <input type="url" placeholder="Digite a URL de uma imagem" />

      <label for="selectDifficulty">Selecione a dificuldade da questão *</label>
      <select name="selectDifficulty" v-model="questionToEdit.difficulty">
        <option value="easy">Fácil</option>
        <option value="medium">Médio</option>
        <option value="hard">Difícil</option>
      </select>
      <label for="selectTheme">Selecione o tema da pergunta *</label>
      <select name="selectTheme" v-model="questionToEdit.theme">
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
        <button type="submit">Editar</button>
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
  name: "EditModal",
  data() {
    return {
		};
  },
  methods: {
    async editQuestion(e) {
      e.preventDefault();

      let questionObject = {
        id: this.questionToEdit.id,
        question: this.questionToEdit.question,
        alternatives: [
					{ alternative: 'A', answer: this.answerA },
					{ alternative: 'B', answer: this.answerB },
					{ alternative: 'C', answer: this.answerC },
					{ alternative: 'D', answer: this.answerD },
				],
        correctAnswer: this.questionToEdit.correctAnswer,
        difficulty: this.questionToEdit.difficulty,
        theme: this.questionToEdit.theme,
      };

      const data = await axios
        .put(
          `https://quiz-api-jgsl.herokuapp.com/questions/${this.questionToEdit.id}`,
          questionObject
        )
        .then(() => {
          Toast.fire({
						icon: 'success',
						title: 'Questão editada com sucesso.'
					})
        })
        .catch((e) => {
          console.log(e);
        });

      this.$emit("loadApi");
			this.$emit('setModal')
    },
    changeCorrectAnswer(correctAnswer) {
      this.questionToEdit.correctAnswer = correctAnswer;
    }
  },
  props: {
    idEditModal: String,
    questionToEdit: Object,
		answerA: String,
		answerB: String,
		answerC: String,
		answerD: String,
  },
  emits: ["setModal", "loadApi", "loadQuestion"],
};
</script>

<style lang="sass" src="./style.scss" scoped></style>
