<template>
    <div class="containerAdmin">
      <header>
        <h1>Admin</h1>
        <div class="infoUserAdmin">
          <span>João Guilherme</span>
          <div></div>
        </div>
      </header>

      <div class="contentCardsInfos">
        <div class="cardInfo">
          <h2>Questões</h2>
          <span>{{ String(arrayQuestions.length).padStart(2,"0") }}</span>
        </div>
        <div class="cardInfo">
          <h2>Usuários</h2>
          <span>00</span>
        </div>
        <div class="cardInfo">
          <h2>Sugestões</h2>
          <span>00</span>
        </div>
        <div class="cardInfo">
          <h2>Open</h2>
          <span>00</span>
        </div>
      </div>

      <Table @reloadAdmin="loadApi" />
    </div>
</template>

<script>
import axios from "axios";
import Sidebar from "../Sidebar/sidebar.vue";

import Table from "./Table/table.vue";

export default {
  name: "Admin",
  data() {
    return {
      arrayQuestions: [],

	  state: ""
    };
  },
  methods: {
    async loadApi() {
      const data = await axios.get("https://quiz-api-jgsl.herokuapp.com/questions");
      this.arrayQuestions = data.data;	
    }
  },
  mounted() {
    this.loadApi();
  },
  components: {
    Sidebar,
    Table,
  },
};
</script>

<style lang="sass" src="./style.scss" scoped></style>
