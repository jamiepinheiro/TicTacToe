<template>
	<div>
		<h1>Healthy Vs Unhealthy Food Tic-Tac-Toe</h1>
		<h3 class="mb-3">
			<span :class="{'text-light bg-success': currentPlayer == 0}">{{players[0]}}</span> 
			vs 
			<span :class="{'text-light bg-success': currentPlayer == 1}">{{players[1]}}</span>
		</h3>
		<table class="col-md-4 col-sm-10 mx-auto">
			<tr v-for="y in indexes" :key=y>
				<td v-for="x in indexes" :key=x>
					<cell :coordinates="[x, y]" :clickCell="clickCell" :val="board[y][x]"></cell>
				</td>
			</tr>
		</table>
	</div>

</template>

<script>
import Cell from './Cell.vue'

export default {
	props: ['players'],
	data() {
		return {
			currentPlayer: 0,
			board: Array(3).fill().map(()=>Array(3).fill('')), //3 by 3 matrix that will store game data
			indexes: [0, 1, 2],
			options: ['d', 'c'],
			gameover: false
		}
	},
	components: {
		Cell
	},
	methods: {
		// Executed by a cell when it is marked by a player
		clickCell(coordinates) {
			if (this.board[coordinates[1]][coordinates[0]] === ''){
				this.board[coordinates[1]][coordinates[0]] = this.options[this.currentPlayer];
				this.currentPlayer = this.currentPlayer == 1 ? 0 : 1;
				this.checkGameover();
			}
		},
		checkGameover() {

		}
	}
}
</script>

<style scoped>
	table {
		width: 90%;
	}
	td {
		width: 33.33%;
		position: relative;
		border: black;
		border-style: solid;
	}
	td:after {
		content: '';
		display: block;
		margin-top: 100%;
	}
</style>
