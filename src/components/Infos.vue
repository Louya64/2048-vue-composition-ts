<template>
	<div class="infos">
		<p>infos</p>
	</div>
</template>

<script setup lang="ts">
//////  imports   //////
// import { ref, onMounted, onUnmounted, reactive, computed } from "vue";

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
.infos {
	background-color: aquamarine;
	height: 20%;
}
</style>
