<template>
	<div>
		<h1>Game</h1>
		<h4 class="mb-3">
			<span :class="{'font-weight-bold': currentPlayer == 0}">{{players[0]}}</span> 
			vs 
			<span :class="{'font-weight-bold': currentPlayer == 1}">{{players[1]}}</span>
		</h4>
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
	props: ["players"],
	data() {
		return {
			currentPlayer: 0,
			board: Array(3).fill().map(()=>Array(3).fill()),
			indexes: [0, 1, 2],
			options: ['d', 'c']
		}
	},
	components: {
		Cell
	},
	methods: {
		clickCell(coordinates) {
			this.board[coordinates[1]][coordinates[0]] = this.options[this.currentPlayer];
			this.currentPlayer = this.currentPlayer == 1 ? 0 : 1;
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
