<template>
	<div class="col-12">
		<div class="col-md-4 col-sm-10 alert alert-success mx-auto m-5 p-3">
			<h2>Game Over!</h2>
			<h3 v-if="draw">Its a draw 😔</h3>
			<h3 v-else> {{winner}} has won 🎉🎉</h3>
			<button @click="restart()" class="btn btn-primary col-6 p-2">Restart</button>
		</div>
	</div>
</template>

<script>
export default {
	props: ["winner", "restart", "draw"]
}
</script>

<style>

</style>
