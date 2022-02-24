<template>
	<button class="btn" @click="start">Start</button>
	<div class="grid">
		<div class="row" v-for="row in gridContent">
			<GameCell
				v-for="(cell, index) in row"
				:colLength="colLength"
				:key="index"
				:content="cell"
			/>
		</div>
	</div>
	<!-- <div v-if="gridTemplate.length" class="grid">
		<GameCell
			v-for="(cell, index) in gridTemplate"
			:colLength="colLength"
			:cell="cell"
			:key="index"
			:content="cell.numberValue"
		/>
	</div> -->
</template>

<script setup lang="ts">
import { ref, reactive, onBeforeMount } from "vue";
import GameCell from "./GameCell.vue";

interface Cell {
	row: number;
	col: number;
	numberValue: number;
}

const colLength = ref(4);
const rowLength = ref(4);
let gridTemplate = reactive([] as Cell[]);
let gridContent = reactive([] as number[][]);

onBeforeMount(() => {
	for (let i = 0; i < rowLength.value; i++) {
		gridContent.push([]);
		for (let j = 0; j < colLength.value; j++) {
			gridContent[i].push(0);
			gridTemplate.push({ row: i, col: j, numberValue: 0 });
		}
	}
});

const start = () => {
	gridTemplate.map((cell) => (cell.numberValue = 0));
	gridContent.map((row) => row.map(() => 0));
	fillRandomCell();
	fillRandomCell();
	window.addEventListener("keydown", (e) => {
		e.preventDefault();
		if (
			e.key === "ArrowUp" ||
			e.key === "ArrowRight" ||
			e.key === "ArrowDown" ||
			e.key === "ArrowLeft"
		) {
			move(e.key);
		}
	});
};

const fillRandomCell = () => {
	let emptyCells = [] as { row: number; col: number }[];

	gridContent.map((row, indexRow) =>
		row.map((cell, indexCell) => {
			if (gridContent[indexRow][indexCell] === 0) {
				emptyCells.push({ row: indexRow, col: indexCell });
			}
		})
	);

	const randomNum = Math.floor(Math.random() * emptyCells.length);
	gridContent[emptyCells[randomNum].row][emptyCells[randomNum].col] =
		randomPopNumber();

	// const emptyCells: Cell[] = gridTemplate.filter(
	// 	(cell) => cell.numberValue === 0
	// );
	// const randomNum = Math.floor(Math.random() * emptyCells.length);
	// emptyCells[randomNum].numberValue = randomPopNumber();
	// const cell = gridTemplate.find(
	// 	(c) =>
	// 		c.row === emptyCells[randomNum].row && c.col === emptyCells[randomNum].col
	// );
	// if (cell) {
	// 	gridTemplate.splice(gridTemplate.indexOf(cell), 1, emptyCells[randomNum]);
	// }
};

const randomPopNumber = () => {
	if (Math.random() > 0.85) {
		return 4;
	}
	return 2;
};

const move = (arrow: string) => {
	// ArrowUp => row - 1
	if (arrow === "ArrowUp") {
		// let somethingUpEmpty = true;
		// while (somethingUpEmpty) {
		// somethingUpEmpty = false;
		// if (change) => somethingUpEmpty = true;
		// }
		for (let i = 1; i < rowLength.value; i++) {
			for (let j = 0; j < colLength.value; j++) {
				if (gridContent[i - 1][j] === 0) {
					gridContent[i - 1][j] = gridContent[i][j];
					gridContent[i][j] = 0;
				}
			}
		}
	}

	// console.log(arrow);
	// for (let i = 1; i < rowLength.value; i++) {
	// 	for (let j = 0; j < colLength.value; j++) {
	// 		if (gridTemplate {row:i-1, col:j} => numberValue === 0)
	// 	}
	// }
	// gridTemplate.map((cell) => {
	// 	console.log(cell)
	// 	});
	// ArrowUp => row - 1
	// ArrowDown => row +1
	// ArrowLeft => col -1
	// ArrowRight => col +1
};

// const showKey = (e: Event) => {
// 	e.preventDefault();
// 	console.log(e);
// };

// const arrowUp = () => {
// 	console.log("up");
// };

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
</script>

<style>
.grid {
	background-color: rgb(205, 193, 180);
	border: 5px solid rgb(187, 173, 160);
	width: 25vw;
	height: 25vw;
	margin: 0 auto;
	/* display: flex;
	flex-wrap: wrap; */
}
.row {
	display: flex;
	height: 25%;
}
</style>
