<template>
	<div>
		<h1>Game</h1>
		<h4 class="mb-3">{{player1}} vs {{player2}}</h4>
		<table class="col-md-4 col-sm-10 mx-auto">
			<tr>
				<td><cell :coodinates="[0, 0]"></cell></td>
				<td><cell :coodinates="[1, 0]"></cell></td>
				<td><cell :coodinates="[2, 0]"></cell></td>
			</tr>
			<tr>
				<td><cell :coodinates="[0, 1]"></cell></td>
				<td><cell :coodinates="[1, 1]"></cell></td>
				<td><cell :coodinates="[2, 1]"></cell></td>
			</tr>
			<tr>
				<td><cell :coodinates="[0, 2]"></cell></td>
				<td><cell :coodinates="[1, 2]"></cell></td>
				<td><cell :coodinates="[2, 2]"></cell></td>
			</tr>
		</table>
	</div>

</template>

<script>
import Cell from './Cell.vue'

export default {
	props: ["player1", "player2"],
	data() {
		currentPlayer = 0
	},
	components: {
		Cell
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
