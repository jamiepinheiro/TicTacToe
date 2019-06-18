<template>
	<h3 class="col-md-3 col-sm-10 mx-auto mb-3 p-3 bg-primary text-white">
			<span :class="{'font-weight-bold': currentPlayer == 0}">{{players[0]}}</span> 
			vs 
			<span :class="{'font-weight-bold': currentPlayer == 1}">{{players[1]}}</span>
		</h3>
</template>

<script>
export default {
	props: ["currentPlayer", "players"]
}
</script>

<style>

</style>
