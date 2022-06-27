<template>
	<div class="containerPlay">
		<header>
        <h1>Jogar</h1>
        <div class="infoUserAdmin">
          <span>João Guilherme</span>
          <div></div>
        </div>
      </header>

	  <div class="flexCardsPlayGame">
		  <button class="cardPlayGame">
			  <span>Geral</span>
			  <i class='bx bx-play'></i>
		  </button>
		  <button class="cardPlayGame">
			  <span>Programação</span>
			  <i class='bx bx-code-curly'></i>
		  </button>
		  <button class="cardPlayGame">
			  <span>Inglês</span>
			  <i class='bx bxs-book-content' ></i>
		  </button>
		  <button class="cardPlayGame">
			  <span>Cinema</span>
			  <i class='bx bxs-movie-play' ></i>
		  </button>
		  <button class="cardPlayGame">
			  <span>História</span>
			  <i class='bx bx-book-reader'></i>
		  </button>
		  <button class="cardPlayGame">
			  <span>Matemática</span>
			  <i class='bx bx-math' ></i>
		  </button>
		  <button class="cardPlayGame">
			  <span>Ciências</span>
			  <i class='bx bxs-flask'></i>
		  </button>
		  <button class="cardPlayGame">
			  <span>Esportes</span>
			  <i class='bx bx-football' ></i>
		  </button>
	  </div>
	</div>
</template>

<script>

export default {
    name: 'Play',
    data() {
        return {

        }
    }, 
    components: {
    
    }
}
</script>

<style lang="sass" src="./style.scss" scoped></style>