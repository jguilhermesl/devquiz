<template>
    <div class="sidebar" :class="{ sidebarOff: isSidebar === false}">
        <span>
            <div class="logo">
            </div>
            <span>Dashboard Devquiz</span>
        </span>
        <ul>
            <router-link to="/play"><i class='bx bx-play' style="font-size: 1.3rem"></i> Jogar</router-link>
            <router-link to="/"><i class='bx bxs-bar-chart-alt-2' style="font-size: 1.3rem"></i> Ranking</router-link>
            <router-link to="/"><i class='bx bx-bulb' style="font-size: 1.3rem"></i> Sugestão</router-link>
            <router-link to="/"><i class='bx bx-question-mark' style="font-size: 1.3rem"></i> Como jogar</router-link>
        </ul>
        <div class="line"></div>
        <ul class="listConfig"> 
            <router-link to="/"><i class='bx bxs-user'></i> Perfil</router-link>
            <router-link to="/admin"><i class='bx bx-lock-alt'></i> Área admin</router-link>
        </ul> 

		<button class="setSidebar" @click="$emit('setSidebar')">
			<i class='bx bx-chevron-left' v-show="isSidebar"></i>
			<i class='bx bx-chevron-right' v-show="isSidebar === false"></i>
		</button>
    </div>
</template>

<script>
import { mdiAirplaneCog } from '@mdi/js'

export default {
    name: 'Sidebar',
	data() {
		return {
			
		}
	},
	props: {
		isSidebar: Boolean,
	},
	emits: ['setSidebar'],
	components: {

	}
}
</script>

<style src="./style.scss" lang="sass" scoped></style>