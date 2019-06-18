<template>
	<div 
		@click="clickCell(coordinates)"
		:class="{ 
			donut: val == 'd',
			cinnamon: val == 'c',
			clickableDonut: val == '' && gameActive && nextMove == 'd',
			clickableCinnamon: val == '' && gameActive && nextMove == 'c',
			highlighted: highlighted
			}">
	</div>
</template>

<script>

export default {
	props: ["coordinates", "clickCell", "val", "gameActive", "nextMove", "highlighted"],
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

	.clickableDonut:hover {
		opacity: 0.2;
		background-image: url("../assets/donut.svg");
		cursor: pointer;
	}

	.clickableCinnamon:hover {
		opacity: 0.2;
		background-image: url("../assets/cinnamon.svg");
		cursor: pointer;
	}

	.highlighted {
		background-color: rgba(0, 255, 55, 0.24)
	}
</style>
