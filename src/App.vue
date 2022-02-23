<template>
	<h1>2048</h1>
	<div class="wrapper">
		<Infos />
		<GameGrid />
	</div>
</template>

<script setup lang="ts">
import Infos from "./components/Infos.vue";
import GameGrid from "./components/GameGrid.vue";

// let truc = "machin";
// truc = "bidule";

// const editEmit = (data: string) => {
// 	console.log(data);
// };

// const faitUnTruc = () => {
// 	console.log("fait un truc");
// };

///// emit /////
// type-based
// const emit = defineEmits<{
//   (e: 'change', id: number): void
//   (e: 'update', value: string): void
// }>()

///// ref ////
// import { ref, onMounted } from 'vue'
// const el = ref<HTMLInputElement | null>(null)
// onMounted(() => {
//   el.value?.focus()
// })
//----------
// const isContentShown = ref(false)
// const open = () => (isContentShown.value = true)
// defineExpose({
//   open
// })
</script>

<style>
@import "./assets/base.css";

#app {
	background-color: rgb(250, 248, 239);
	margin: 0 auto;
	padding: 2rem;
	text-align: center;
	font-weight: normal;
}
.wrapper {
	width: 50vw;
	height: 50vw;
	display: flex;
	flex-direction: column;
	margin: auto;
}
.btn {
	background-color: rgb(143, 122, 102);
	color: rgb(250, 248, 239);
}
</style>
