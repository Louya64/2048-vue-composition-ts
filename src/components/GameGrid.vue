<template>
	<button class="btn" @click="start">Start</button>
	<p>score : {{ score }}</p>
	<div class="grid">
		<div class="row" v-for="(row, rowIndex) in gridContent">
			<GameCell
				v-for="(cell, cellIndex) in row"
				:colLength="colLength"
				:key="rowIndex.toString() + cellIndex.toString()"
				:content="cell"
			/>
		</div>
	</div>
</template>

<script setup lang="ts">
import { ref, reactive, onBeforeMount } from "vue";
import GameCell from "./GameCell.vue";

const colLength = ref(4);
const rowLength = ref(4);
let gridContent = reactive([] as number[][]);
let score = ref(0);

onBeforeMount(() => {
	for (let i = 0; i < rowLength.value; i++) {
		gridContent.push([]);
		for (let j = 0; j < colLength.value; j++) {
			gridContent[i].push(0);
		}
	}
});

const start = () => {
	gridContent[0] = [4, 0, 0, 0];
	gridContent[1] = [4, 0, 0, 0];
	gridContent[2] = [2, 0, 0, 0];
	gridContent[3] = [2, 0, 0, 0];
	// gridContent.map(
	// 	(row, rowIndex) => (gridContent[rowIndex] = row.map(() => 0))
	// );

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
		const moveUp = () => {
			for (let i = 1; i < rowLength.value; i++) {
				for (let j = 0; j < colLength.value; j++) {
					if (gridContent[i][j] !== 0) {
						let k = i - 1;
						while (k > -1 && gridContent[k][j] === 0) {
							k--;
						}
						const temp = gridContent[i][j];
						gridContent[i][j] = 0;
						gridContent[k + 1][j] = temp;
					}
				}
			}
		};
		const mergeUp = () => {
			for (let i = 1; i < rowLength.value; i++) {
				for (let j = 0; j < colLength.value; j++) {
					if (gridContent[i - 1][j] === gridContent[i][j]) {
						score.value += gridContent[i - 1][j] * 2;
						gridContent[i - 1][j] = gridContent[i - 1][j] * 2;
						gridContent[i][j] = 0;
					}
				}
			}
		};

		moveUp();
		mergeUp();
		moveUp();
		fillRandomCell();
	}

	// ArrowDown => row +1
	if (arrow === "ArrowDown") {
		const moveDown = () => {
			for (let i = rowLength.value - 2; i > -1; i--) {
				for (let j = 0; j < colLength.value; j++) {
					if (gridContent[i][j] !== 0) {
						let k = i + 1;
						while (k < rowLength.value && gridContent[k][j] === 0) {
							k++;
						}
						const temp = gridContent[i][j];
						gridContent[i][j] = 0;
						gridContent[k - 1][j] = temp;
					}
				}
			}
		};
		const mergeDown = () => {
			for (let i = rowLength.value - 2; i > -1; i--) {
				for (let j = 0; j < colLength.value; j++) {
					if (gridContent[i + 1][j] === gridContent[i][j]) {
						score.value += gridContent[i + 1][j] * 2;
						gridContent[i + 1][j] = gridContent[i + 1][j] * 2;
						gridContent[i][j] = 0;
					}
				}
			}
		};

		moveDown();
		mergeDown();
		moveDown();
		fillRandomCell();
	}

	// ArrowLeft => col -1
	if (arrow === "ArrowLeft") {
		const moveDown = () => {
			for (let i = 0; i < rowLength.value; i++) {
				for (let j = 1; j < colLength.value; j++) {
					if (gridContent[i][j] !== 0) {
						let k = j - 1;
						while (k > -1 && gridContent[i][k] === 0) {
							k--;
						}
						const temp = gridContent[i][j];
						gridContent[i][j] = 0;
						gridContent[i][k + 1] = temp;
					}
				}
			}
		};
		const mergeDown = () => {
			for (let i = 0; i < rowLength.value; i++) {
				for (let j = 1; j < colLength.value; j++) {
					if (gridContent[i][j - 1] === gridContent[i][j]) {
						score.value += gridContent[i][j - 1] * 2;
						gridContent[i][j - 1] = gridContent[i][j - 1] * 2;
						gridContent[i][j] = 0;
					}
				}
			}
		};

		moveDown();
		mergeDown();
		moveDown();
		fillRandomCell();
	}

	// ArrowRight => col +1
	if (arrow === "ArrowRight") {
		let haveMoved = false;
		const moveDown = () => {
			for (let i = 0; i < rowLength.value; i++) {
				for (let j = colLength.value - 2; j > -1; j--) {
					if (gridContent[i][j] !== 0) {
						let k = j + 1;
						while (k < rowLength.value && gridContent[i][k] === 0) {
							haveMoved = true;
							k++;
						}
						const temp = gridContent[i][j];
						gridContent[i][j] = 0;
						gridContent[i][k - 1] = temp;
					}
				}
			}
		};
		const mergeDown = () => {
			for (let i = 0; i < rowLength.value; i++) {
				for (let j = colLength.value - 2; j > -1; j--) {
					if (gridContent[i][j + 1] === gridContent[i][j]) {
						haveMoved = true;
						score.value += gridContent[i][j + 1] * 2;
						gridContent[i][j + 1] = gridContent[i][j + 1] * 2;
						gridContent[i][j] = 0;
					}
				}
			}
		};

		moveDown();
		mergeDown();
		moveDown();
		if (haveMoved) {
			fillRandomCell();
		}
	}
};
</script>

<style>
.grid {
	background-color: rgb(205, 193, 180);
	border: 5px solid rgb(187, 173, 160);
	width: 25vw;
	height: 25vw;
	margin: 0 auto;
	border-radius: 5px;
}
.row {
	display: flex;
	height: 25%;
}
</style>
