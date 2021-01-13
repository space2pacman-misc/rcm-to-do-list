<template>
	<div>
		<div class="header">Add new one</div>
		<div class="form">
			<input type="text" class="form__control" placeholder="TITLE" v-model="task.title">
			<textarea class="form__control form__textarea" placeholder="DESCRIPTION" v-model="task.description"></textarea>
			<select class="form__control" v-model="task.term">
				<option>TODAY</option>
				<option>TOMORROW</option>
			</select>
			<div class="text-center">
				<button type="button" class="button" @click="addTask">Add</button>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			task: {
				title: "",
				description: "",
				completed: false,
				term: "TODAY"
			}
		}
	},
	methods: {
		addTask() {
			this.$emit("onAddTask", this.task);
			this.clearTaskInputs();
		},
		clearTaskInputs() {
			this.task.title = "";
			this.task.description = "";
		}
	}
}
</script>