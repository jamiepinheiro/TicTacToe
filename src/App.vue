<template>
	<div id="app">
		<h1 class="mb-3 jumbotron bg">Healthy Vs Unhealthy Food Tic-Tac-Toe</h1>
		<zoom-center-transition>
			<SelectGame v-if="!inGame" :startGame="startGame" :key="1"></SelectGame>
			<Game v-if="inGame" :players="players" :restart="restart" :key="2"/>
		</zoom-center-transition>
	</div>
</template>

<script>
import Game from './components/Game.vue'
import SelectGame from './components/SelectGame.vue'

export default {
	data() {
		return {
			players: [],
			inGame: false,
		}
	},
	components: {
		Game,
		SelectGame
	},
	methods: {
		startGame(mode) {
			if (mode == "pvp") {
				this.players = ['Player 1', 'Player 2']
			} else if (mode == "pva") {
				this.players = ['Player 1', 'AI']
			}
			this.inGame = true;
		},
		restart() {
			this.inGame = false;
		}
	}
}
</script>

<style>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
}

.bg {
	color: white;
	background: linear-gradient(to right, rgb(7, 185, 255) , rgb(4, 255, 138));
	border-radius: 0%;
}
</style>
