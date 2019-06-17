<template>
	<div 
	@click="clickCell(coordinates)"
	:class="{ donut: val=='d', cinnamon: val=='c', clickable: val == ''}">
	</div>
</template>

<script>

export default {
	props: ["coordinates", "clickCell", "val"],
	data() {
		return {
			donut: false,
			cinnamon: false
		}
	}
}
</script>

<style scoped>
	div{
		position: absolute;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
	}
	.donut {
		background-image: url("../assets/donut.svg");
	}
	.cinnamon {
		background-image: url("../assets/cinnamon.svg");
	}

	.clickable:hover {
		background-color: #eeeeee;
		cursor: pointer;
	}
</style>
