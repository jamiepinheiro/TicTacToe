<template>
	<div>
		<div class="jumbotron">
			<h1>Healthy Vs Unhealthy Food Tic-Tac-Toe</h1>
			<h3 class="mb-3">
			<span :class="{'text-light bg-success': currentPlayer == 0}">{{players[0]}}</span> 
			vs 
			<span :class="{'text-light bg-success': currentPlayer == 1}">{{players[1]}}</span>
			</h3>
		</div>
		
		<table class="col-md-4 col-sm-10 mx-auto">
			<tr v-for="y in indexes" :key=y>
				<td v-for="x in indexes" :key=x>
					<cell 
						:coordinates="[x, y]"
						:clickCell="clickCell"
						:val="board[y][x]"
						:gameActive="!gameover"
						:nextMove="options[currentPlayer]">
					</cell>
				</td>
			</tr>
		</table>
		<div v-if="gameover" class="col-12">
			<div class="col-md-4 col-sm-10 alert alert-info mx-auto m-5 p-3">
				<h2>Game Over!</h2>
				<h3 v-if="draw">Its a draw!</h3>
				<h3 v-else> {{players[currentPlayer]}} has won 🎉🎉</h3>
			</div>
		</div>
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
			gameover: false,
			draw: false
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
			// Possible '3 in a rows' that could lead to gameover state
			const row = this.board[coordinates[1]]
			const col = [this.board[0][coordinates[0]], this.board[1][coordinates[0]], this.board[2][coordinates[0]]];
			const diag1 = [this.board[0][0], this.board[1][1], this.board[2][2]];
			const diag2 = [this.board[0][2], this.board[1][1], this.board[2][0]];
			const possible3Rows = [row, col];

			// Only need to check the diagonals if the marked cell was on one
			if (diag1.includes(coordinates))
				possible3Rows.push(diag1);
			if (diag2.includes(coordinates))
				possible3Rows.push(diag2);

			// Check each row to see if its a winning row
			for (let i = 0; i < possible3Rows.length; i++) {
				if (new Set(possible3Rows[i]).size === 1) {
					this.gameover = true;
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
