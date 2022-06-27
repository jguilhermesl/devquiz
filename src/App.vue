<template>
  <Sidebar :isSidebar="isSidebar" @setSidebar="setSidebar"/>
  <div class="containerComponent" :class="{ containerComponentWithoutSidebar: isSidebar === false}">
    <router-view />
  </div>
</template>

<script>
import Sidebar from "./components/Sidebar/sidebar.vue";

export default {
  name: "App",
  components: {
    Sidebar,
  },
  data() {
	  return {
		  isSidebar: true
	  }
  },
  methods: {
	  setSidebar() {
		  this.isSidebar = !this.isSidebar
	  }
  }
};
</script>


<style src="./styles/globalStyles.scss"></style>
