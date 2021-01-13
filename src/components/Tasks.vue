<template>
	<div>
		<div class="header">My {{ caption }} todo</div>
		<div class="tasks" v-for="(task, index) in tasks" :key="index">
			<div class="task">
				<div class="task__header">
					<div class="task__title">{{ task.title }}</div>
					<div class="task__controls">
						<div class="task__action task__icon-check" :class="{'background__blue': !task.completed}" @click="complet(task)"></div>
						<div class="task__action task__icon-close background__red" @click="remove(index)"></div>
					</div>
				</div>
				<div v-if="task.description" class="task__description">{{ task.description }}</div>
			</div>
		</div>
		<slot name="button"></slot>
		<div class="tasks__empty" v-if="tasks.length === 0">There are no tasks for {{ caption }}</div>
	</div>
</template>

<script>
export default {
	methods: {
		complet(task) {
			task.completed = !task.completed;
		},
		remove(index) {
			this.tasks.splice(index, 1);
		}
	},
	props: {
		caption: String,
		tasks: Array
	}
}
</script>