<template>
	<section>
		<base-card>
			<h2>Record research projects that interest you</h2>

			<form @submit.prevent="submitSurvey">
				<div class="form-control">
					<label for="name"> Supervisors Name</label>
					<input type="text" id="name" name="name" v-model.trim="enteredName" />
				</div>
				<div class="form-control">
					<label for="project"> Project</label>
					<input type="text" id="project" name="project" v-model.trim="enteredProject" />
				</div>
				<div class="form-control">
					<label for="university"> University</label>
					<input type="text" id="university" name="university" v-model.trim="enteredUniversity" />
				</div>

				<div class="form-control">
					<label for="email"> Supervisor Email</label>
					<input type="text" id="email" name="email" v-model.trim="enteredEmail" />
				</div>

				<h3>My Level of satisfaction ... </h3>
				<div class="form-control">
					<input type="radio" id="rating-poor" value="poor" name="rating" v-model="chosenRating" />
					<label for="rating-poor">Poor</label>
				</div>

				<div class="form-control">
					<input type="radio" id="rating-average" value="average" name="rating" v-model="chosenRating" />
					<label for="rating-average">Average</label>
				</div>

				<div class="form-control">
					<input type="radio" id="rating-great" value="great" name="rating" v-model="chosenRating" />
					<label for="rating-great">Great</label>
				</div>

				<p v-if="invalidInput">
					One or more input fields are invalid. Please check your
					provided data.
				</p>

				<p v-if="error">{{ error }}</p>

				<div>
					<base-button>Submit</base-button>
				</div>
			</form>
		</base-card>
	</section>
</template>

<script>
// import axios from 'axios';

export default {
	data() {
		return {
			enteredName: '',
			enteredProject: '',
			enteredUniversity:'',
			enteredEmail:'',
			chosenRating: null,
			invalidInput: false,
			error: null
		};
	},

	methods: {
		submitSurvey() {
			if (this.enteredName === '' || !this.chosenRating) {
				this.invalidInput = true;
				return;
			}
			this.invalidInput = false;
			this.error = null;


			fetch('https://vue-h-demo-default-rtdb.europe-west1.firebasedatabase.app/surveys.json', {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json'
				},
				body: JSON.stringify({
					name: this.enteredName,
					project: this.enteredProject,
					university: this.enteredUniversity,
					email: this.enteredEmail,
					rating: this.chosenRating,
				}),
			}).then(response => {
				if (response.ok) {
					//...
				} else {
					throw new Error('Could not save data!');
				}
			}).catch((error) => {
				console.log(error);
				this.error = error.message;
			});

			// this.enteredName = '';
			// this.chosenRating = null;
			// .then((res) => {
			// 	if (res.ok) {
			// 		//
			// 	} else {
			// 		throw new Error('could not save data!');
			// 	}
			// })
			// .catch((error) => {
			// 	console.log(error);
			// 	this.error = error.message;
			// });



		}
	}

}
</script>

<style scoped>
.form-control {
	margin: 0.5rem 0;
}

input[type='text'] {
	display: block;
	width: 20rem;
	margin-top: 0.5rem;
}
</style>