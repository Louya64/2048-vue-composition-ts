<template>
	<button class="btn" @click="start">Start</button>
	<div class="grid">
		<div
			:style="{ height: `${100 / rowLength}%` }"
			class="row"
			v-for="row in rowLength"
		>
			<GameCell
				:colLength="colLength"
				v-for="col in colLength"
				:pos="{ row: row, col: col }"
				:num-val="numVal"
			/>
		</div>
	</div>
</template>

<script setup lang="ts">
//////  imports   //////
// import { ref, onMounted, onUnmounted, reactive, computed, watch } from "vue";
import { ref } from "vue";
import GameCell from "./GameCell.vue";

const colLength = ref(4);
const rowLength = ref(4);
const numVal = ref(0);

const randomPopNumber = () => {
	if (Math.random() > 0.85) {
		return 4;
	}
	return 2;
};

const start = () => {
	numVal.value = 0;
	const cell1 = randomPopNumber();
	console.log(cell1);
	const cell2 = randomPopNumber();
	console.log(cell2);
};
const two = () => {
	numVal.value = 2;
};
const four = () => {
	numVal.value = 4;
};
const eight = () => {
	numVal.value = 8;
};
const ten = () => {
	numVal.value = 16;
};
const thirty = () => {
	numVal.value = 32;
};
const hundred = () => {
	numVal.value = 128;
};

// const showKey = (e: Event) => {
// 	e.preventDefault();
// 	console.log(e);
// };

// const arrowUp = () => {
// 	console.log("up");
// };

///////  props  /////////
// interface Props {
// 	truc: string;
// }
// const props = defineProps<Props>();
// const truc = props.truc;

/////////  emits /////////
// const emit = defineEmits<{
// 	(e: "emitFromChild", message: string): void;
// 	(e: "autreEmit"): void;
// }>();
/////////////////////////
// const emitFunc = () => {
// 	emit("autreEmit");
// };

////////////   computed  ///////////////
// const publishedBooksMessage = computed(() => {
//   return author.books.length > 0 ? 'Yes' : 'No'
// })

//////// lifecycle hooks:  callback ///////
// onMounted(() => console.log("mounted"));
</script>

<style>
.grid {
	background-color: rgb(205, 193, 180);
	border: 5px solid rgb(187, 173, 160);
	width: 25vw;
	height: 25vw;
	margin: 0 auto;
}
.row {
	display: flex;
}
</style>
