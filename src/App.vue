<template>
	<main>
		<!-- heading -->
		<header>
			<img src="https://pinia.vuejs.org/logo.svg" alt="pinia logo" />
			<h1>Pinia Tasks</h1>
		</header>
		<div class="new-task-form">
			<TaskForm />
		</div>
		<nav class="filter">
			<button @click="filter = 'all'">All tasks</button>
			<button @click="filter = 'favs'">Fav tasks</button>
		</nav>
		<div class="loading" v-if="loading">Loading tasks...</div>
		<div v-if="filter === 'all'" class="task-list">
			<p v-if="!loading">You have {{ totalCount }} tasks left to do.</p>
			<div v-for="task in tasks" :key="task.id">
				<TaskDetail :task="task" />
			</div>
		</div>
		<div v-if="filter === 'favs'" class="task-list">
			<p v-if="!loading">You have {{ favCount }} tasks in your favs list.</p>
			<div v-for="task in favs" :key="task.id">
				<TaskDetail :task="task" />
			</div>
		</div>
	</main>
</template>

<script setup>
	import { useTaskStore } from "./stores/TaskStore";
	import TaskDetail from "./components/TaskDetail.vue";
	import TaskForm from "./components/TaskForm.vue";
	import { ref } from "vue";
	import { storeToRefs } from "pinia";
	const taskStore = useTaskStore();

	const {
		tasks,
		loading,
		getTasks,
		addTask,
		deleteTask,
		toggleFav,
		favs,
		favCount,
		totalCount,
	} = storeToRefs(taskStore);
	const filter = ref("all");
	taskStore.getTasks();
</script>
