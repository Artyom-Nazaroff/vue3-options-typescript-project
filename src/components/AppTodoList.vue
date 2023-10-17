<template>
	<ul class="todo-list">
		<app-todo-item
			v-for="todo in todos"
			:key="todo.id"
			:todo="todo"
			@toggle-todo="toggleTodo"
			@remove-todo="removeTodo"
		/>
	</ul>
</template>

<script lang="ts">
import { Todo } from '@/types/todo'
import { defineComponent, PropType } from 'vue'
import AppTodoItem from './AppTodoItem.vue'

export default defineComponent({
	components: { AppTodoItem },
	props: {
		todos: {
			type: Array as PropType<Todo[]>,
		},
	},
	emits: {
		toggleTodo: (id: number) => Number.isInteger(id),
		removeTodo: (id: number) => Number.isInteger(id),
	},
	methods: {
		toggleTodo(id: number) {
			this.$emit('toggleTodo', id)
		},
		removeTodo(id: number) {
			this.$emit('removeTodo', id)
		}
	},
})
</script>

<style scoped></style>