<template>
	<form @submit.prevent="handleSubmit">
		<input type="text" placeholder="I need to..." v-model="newTask" />
		<button>Add</button>
	</form>
</template>

<script setup>
	import { ref } from "vue";
	import { useTaskStore } from "../stores/TaskStore";

	const newTask = ref("");
	const taskStore = useTaskStore();
	const handleSubmit = () => {
		if (newTask.value.length > 0) {
			taskStore.addTask({
				id: Date.now(),
				title: newTask.value,
				isFav: false,
			});

			newTask.value = "";
		}
	};
</script>
