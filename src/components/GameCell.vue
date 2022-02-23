<template>
	<div :style="{ width: `${100 / colLength}%` }" class="cell">
		<p class="cellPos">cell {{ row }} - {{ col }}</p>

		<div v-if="numVal > 0" :class="valNumToColorClass" class="numVal">
			{{ numVal }}
		</div>
	</div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

interface Pos {
	col: number;
	row: number;
}

interface Props {
	colLength: number; // for style width
	pos: Pos;
	numVal: number; // props? ou dans component?
}
const props = defineProps<Props>();
const colLength = props.colLength;
const col = ref(props.pos.col);
const row = props.pos.row;

const valNumToColorClass = computed(() => {
	switch (props.numVal) {
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
.numVal {
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
