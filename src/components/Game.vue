<template>
	<div>
		<h1 class="my-5">Healthy Vs Unhealthy Food Tic-Tac-Toe</h1>
		<h3 class="mb-3">
			<span :class="{'font-weight-bold': currentPlayer == 0}">{{players[0]}}</span> 
			vs 
			<span :class="{'font-weight-bold': currentPlayer == 1}">{{players[1]}}</span>
		</h3>
		<div v-if="gameover" class="col-12">
			<div class="col-md-4 col-sm-10 alert alert-success mx-auto m-5 p-3">
				<h2>Game Over!</h2>
				<h3 v-if="draw">Its a draw 😔</h3>
				<h3 v-else> {{players[currentPlayer]}} has won 🎉🎉</h3>
				<button @click="restart()" class="btn btn-primary col-6 p-2">Restart</button>
			</div>
		</div>
		<table class="col-md-3 col-sm-10 mx-auto">
			<tr v-for="y in indexes" :key=y>
				<td v-for="x in indexes" :key=x>
					<cell 
						:coordinates="[x, y]"
						:clickCell="clickCell"
						:val="board[y][x]"
						:gameActive="!gameover"
						:nextMove="options[currentPlayer]"
						:highlighted="coordInList([x, y], winningThreeCells)">
					</cell>
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
			indexes: [0, 1, 2],
			options: ['d', 'c'],
			gameover: false,
			draw: false,
			winningThreeCells: [],
			board: Array(3).fill().map(()=>Array(3).fill('')), //3 by 3 matrix that will store game data
		}
	},
	components: {
		Cell
	},
	methods: {
		// Executed by a cell when it is marked by a player
		clickCell(coordinates) {
			if (this.board[coordinates[1]][coordinates[0]] === '' && !this.gameover){
				this.board[coordinates[1]][coordinates[0]] = this.options[this.currentPlayer];
				this.checkGameover(coordinates);
			}
		},
		checkGameover(coordinates) {
			// Possible '3 in a rows' coordinates that could lead to gameover state
			const col = [[coordinates[0], 0], [coordinates[0], 1], [coordinates[0], 2]]
			const row = [[0, coordinates[1]], [1, coordinates[1]], [2, coordinates[1]]]
			const diag1 = [[0, 0], [1, 1], [2, 2]]
			const diag2 = [[0, 2], [1, 1], [2, 0]]
			const possible3Rows = [col, row];

			// Only need to check the diagonals if the marked cell was on one
			if (this.coordInList(coordinates, diag1))
				possible3Rows.push(diag1);
			if (this.coordInList(coordinates, diag2))
				possible3Rows.push(diag2);

			// Check each row to see if its a winning row
			for (let i = 0; i < possible3Rows.length; i++) {
				const rowValues = possible3Rows[i].map(coord => this.board[coord[1]][coord[0]]);
				
				if (new Set(rowValues).size === 1) {
					this.gameover = true;
					this.winningThreeCells = possible3Rows[i];
					return;
				}
			}

			// Check for tie
			if (!this.board.map(row => row.includes('')).includes(true)) {
				this.gameover = true;
				this.draw = true;
			}else {
				this.currentPlayer = this.currentPlayer == 1 ? 0 : 1;
			}
		},
		// Helper that checks if a specific coord is in a list
		coordInList(coord, list) {
			for (let i = 0; i < list.length; i++) {
				if (list[i][0] === coord[0] && list[i][1] === coord[1]) {
					return true;
				}
			}
			return false;
		},
		restart() {
			this.currentPlayer = 0,
			this.board = Array(3).fill().map(()=>Array(3).fill(''));
			this.gameover = false;
			this.draw = false;
			this.winningThreeCells = [];
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
