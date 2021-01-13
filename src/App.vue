<template>
	<div id="app">
		<div class="columns">
			<div class="column background__gray--light">
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
			<div class="column background__gray--strong">
				<Tasks caption="today" :tasks="tasks['today']">
					<div slot="button">
						<button type="button" class="button button__wide" v-if="tasks['today'].length > 0" @click="allTaskComplet('today')">Set all comlite</button>
					</div>
				</Tasks>
			</div>
			<div class="column background__gray--light">
				<Tasks caption="tomorrow" :tasks="tasks['tomorrow']" />
			</div>
		</div>
	</div>
</template>

<script>
import Tasks from "@/components/Tasks";

export default {
	name: "App",
	data() {
		return {
			task: {
				title: "",
				description: "",
				completed: false,
				term: "TODAY"
			},
			tasks: {
				"today": [],
				"tomorrow": []
			}
		}
	},
	methods: {
		addTask() {
			if(this.task.title.length > 0) {
				let task = JSON.parse(JSON.stringify(this.task));

				this.tasks[this.task.term.toLowerCase()].push(task);
				this.clearTaskInputs();
			}
		},
		clearTaskInputs() {
			this.task.title = "";
			this.task.description = "";
		},
		allTaskComplet(term) {
			this.tasks[term] = this.tasks[term].map(task => {
				task.completed = true;

				return task;
			})
		}
	},
	components: {
		Tasks
	}
}
</script>

<style>
body {
	margin: 0;
}

#app {
    max-width: 1000px;
	margin: 0 auto;
	height: 100vh;
	font-family: Arial;
}

.header {
	color: #34596d;
	font-size: 25px;
	font-weight: bold;
	margin-top: 65px;
}

.columns {
	display: flex;
	height: 100%;
}

.column {
	width: 100%;
	box-sizing: border-box;
	padding: 0px 16px;
}

.background__gray--light {
	background-color: #f2f2f2 !important;
}

.background__gray--strong {
	background-color: #c4c4c4 !important;
}

.background__blue {
	background-color: #34596d !important;
}

.background__red {
	background-color: #8b1313 !important;
}

.form {
	margin-top: 43px;
}

.form__control {
	width: 100%;
	box-sizing: border-box;
	border: 1px solid #cdcdcd;
	padding: 10px 6px;
	font-size: 10px;
	margin-bottom: 20px;
}

.form__textarea {
	min-height: 75px;
}

.text-center {
	text-align: center;
}

.button {
	background: #34596d;
	border: none;
	outline: none;
	padding: 12px 40px;
	border-radius: 10px;
	text-transform: uppercase;
	color: #fff;
	font-size: 10px;
	cursor: pointer;
}

.button__wide {
	width: 100%;
}

.tasks {
	margin-top: 40px;
}

.tasks__empty {
	margin-top: 40px;
}

.task {
	background-color: #fff;
	padding: 22px 10px;
	border-radius: 10px;
	font-size: 10px;
	align-items: center;
	margin-bottom: 20px;
    box-shadow: 0px 4px 4px 0px rgb(0 0 0 / .4);
}

.task__action {
	background-color: #dbdbdb;
	width: 18px;
	height: 18px;
	border-radius: 4px;
	margin-right: 5px;
	cursor: pointer;
}

.task__icon-check {
	background-image: url("~@/assets/icon-check.svg");
	background-size: 70%;
	background-repeat: no-repeat;
	background-position: 50% 50%;
}

.task__icon-close {
	background-image: url("~@/assets/icon-close.svg");
	background-size: 65%;
	background-repeat: no-repeat;
	background-position: 50% 50%;
}

.task__header {
	display: flex;
}

.task__title {
	width: 100%;
}

.task__description {
    margin-top: 10px;
}

.task__controls {
	display: flex;
}
</style>