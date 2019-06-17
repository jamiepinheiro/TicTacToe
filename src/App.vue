<template>
	<div id="app">
		<Game :player1="'Player 1'" :player2="'Player 2'"/>
	</div>
</template>

<script>
import Game from './components/Game.vue'

export default {
	name: 'app',
	components: {
		Game
	}
}
</script>

<style>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
