<template>
	<div>
		<h1>Game</h1>
		<h4 class="mb-3">{{player1}} vs {{player2}}</h4>
		<table class="col-md-4 col-sm-10 mx-auto">
			<tr>
				<td><div class="content">1</div></td>
				<td><div class="content">1</div></td>
				<td><div class="content">1</div></td>
			</tr>
			<tr>
				<td><div class="content">1</div></td>
				<td><div class="content">1</div></td>
				<td><div class="content">1</div></td>
			</tr>
			<tr>
				<td><div class="content">1</div></td>
				<td><div class="content">1</div></td>
				<td><div class="content">1</div></td>
			</tr>
		</table>
	</div>

</template>

<script>

export default {
	props: ["player1", "player2"],
	methods: {
		a() {
			console.log(1);
			
		}
	}
}
</script>

<style>
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
	td .content {
		position: absolute;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		background-image: url("../assets/donut.svg");
	}
</style>
