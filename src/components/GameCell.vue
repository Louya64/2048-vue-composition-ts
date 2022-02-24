<template>
	<!-- :style="{ width: `${100 / colLength}%`, height: `${100 / colLength}%` }" -->
	<div :style="{ width: `${100 / colLength}%` }" class="cell">
		<!-- <p class="cellPos">row{{ row }} - col{{ col }}</p> -->

		<div
			v-if="content > 0"
			:class="[{ grow: merged }, valNumToColorClass]"
			class="numberValue"
		>
			{{ content }}
		</div>
	</div>
</template>

<script setup lang="ts">
import { ref, computed, watch } from "vue";

// interface Cell {
// 	row: number;
// 	col: number;
// 	numberValue: number;
// }

interface Props {
	colLength: number; // for style width and height
	// cell: Cell;
	content: number;
}
const props = defineProps<Props>();
const colLength = props.colLength;
const merged = ref(false);

watch(
	() => props.content,
	(newVal, oldVal) => {
		if (newVal === oldVal * 2) {
			merged.value = true;
			setTimeout(() => {
				merged.value = false;
			}, 150);
		}
	}
);

const valNumToColorClass = computed(() => {
	// switch (numberValue) {
	switch (props.content) {
		case 2:
			return "two";
		case 4:
			return "four";
		case 8:
			return "eight";
		case 16:
			return "sixteen";
		case 32:
			return "thirty-two";
		case 64:
			return "sixty-four";
		case 128:
			return "hundred-twenty-eight";
		case 256:
			return "two-hundred-fifty-six";
		case 512:
			return "five-hundred-twelve";
		default:
			console.log("pas de couleur");
	}
});
</script>

<style>
.cell {
	height: 100%;
	border: 5px solid rgb(187, 173, 160);
	position: relative;
}
.cellPos {
	z-index: 1;
}
.numberValue {
	border-radius: 5px;
	position: absolute;
	background-color: burlywood;
	width: 100%;
	height: 100%;
	top: 0;
	display: flex;
	justify-content: center;
	align-items: center;
	font-size: 2vw;
	font-weight: bold;
	color: brown;
	transition: all 20ms;
}
.grow {
	transform: scale(1.1, 1.1);
	transition: all 20ms;
}
.two {
	background-color: rgb(238, 228, 218);
	color: rgb(119, 110, 101);
}
.four {
	background-color: rgb(238, 225, 201);
	color: rgb(119, 110, 101);
}
.eight {
	background-color: rgb(243, 178, 122);
	color: rgb(249, 246, 242);
}
.sixteen {
	background-color: rgb(246, 150, 100);
	color: rgb(249, 246, 242);
}
.thirty-two {
	background-color: rgb(247, 124, 95);
	color: rgb(249, 246, 242);
}
.sixty-four {
	background-color: rgb(247, 95, 59);
	color: rgb(249, 246, 242);
}
.hundred-twenty-eight {
	background-color: rgb(237, 208, 115);
	color: rgb(249, 246, 242);
}
.two-hundred-fifty-six {
	background-color: rgb(237, 204, 98);
	color: rgb(249, 246, 242);
}
.five-hundred-twelve {
	background-color: rgb(237, 201, 80);
	color: rgb(249, 246, 242);
}
</style>
