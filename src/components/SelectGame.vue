<template>
	<div class="col-6 mx-auto bg-light p-3">
		<h3>Select Game Mode</h3>
		<img src="../assets/info.svg" alt="" class="col-7 p-4">
		<br>
		<button @click="startGame('pvp')" class="btn btn-primary col-6 p-2 my-3">Player vs Player</button>
		<br>
		<button @click="startGame('pva')" class="btn btn-danger col-6 p-2">Player vs AI</button>
	</div>
</template>

<script>
export default {
	props: ["startGame"]
}
</script>

