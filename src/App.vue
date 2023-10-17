<template>
	<app-header />
	<app-filters :active-filter="activeFilter" @set-filter="setFilter" />

	<main class="app-main">
		<app-todo-list
			:todos="filteredTodos"
			@toggle-todo="toggleTodo"
			@remove-todo="removeTodo"
		/>

		<app-add-todo @add-todo="addTodo" />
	</main>

	<app-footer />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import AppAddTodo from './components/AppAddTodo.vue'
import AppFilters from './components/AppFilters.vue'
import AppFooter from './components/AppFooter.vue'
import AppHeader from './components/AppHeader.vue'
import AppTodoList from './components/AppTodoList.vue'
import { Filter } from './types/filter'
import { Todo } from './types/todo'

interface State {
	todos: Todo[],
	activeFilter: Filter,
}

export default defineComponent({
	components: {
		AppHeader,
		AppFilters,
		AppTodoList,
		AppAddTodo,
		AppFooter,
	},
	data(): State {
		return {
			todos: [
				{ id: 0, text: 'Learn the basics of Vue', completed: true },
				{ id: 1, text: 'Learn the basics of Typescript', completed: false },
				{ id: 2, text: 'Subscribe to the channel', completed: false },
			],
			activeFilter: 'All',
		}
	},
	computed: {
		filteredTodos(): Todo[] {
			switch (this.activeFilter) {
				case 'Active': return this.todos.filter((el: Todo) => !el.completed)
				case 'Done': return this.todos.filter((el: Todo) => el.completed)
				case 'All':
				default: return this.todos
			}
		}
	},
	methods: {
		toggleTodo(id: number) {
			const targetTodo = this.todos.find((el: Todo) => el.id === id)
			if (targetTodo) targetTodo.completed = !targetTodo.completed
		},
		removeTodo(id: number) {
			this.todos = this.todos.filter((el: Todo) => el.id !== id)
		},
		addTodo(todo: Todo) {
			this.todos.push(todo)
		},
		setFilter(filter: Filter) {
			this.activeFilter = filter
		},
	},
})
</script>

<style scoped></style>