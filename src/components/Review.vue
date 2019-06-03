<template>
	<div id="app">
		<form class="review" @submit.prevent="submit">
			<p v-if="errors.length">
				<b>Please correct the following error(s):</b>
				<ul>
					<li v-for="error in errors">{{ error }}</li>
				</ul>
			</p>

			<p>
				<label for="name">Name:</label>
				<input id="name" v-model="name" placeholder="name">
			</p>

			<p>
				<label for="review">Review:</label>      
				<textarea id="review" v-model="review"></textarea>
			</p>

			<p>
				<label for="rating">Rating:</label>
				<select id="rating" v-model.number="rating">
					<option>5</option>
					<option>4</option>
					<option>3</option>
					<option>2</option>
					<option>1</option>
				</select>
			</p>

			<p>
				<input type="submit" value="Submit">  
			</p>
		</form>
	</div>
</template>

<script>
	export default {
		name: 'Review',
		data() {
			return {
				name: null,
				review: null,
				rating: null,
				errors: []
			}
		},
		methods: {
			submit() {
				this.errors = [];
				
				if (this.name && this.review && this.rating) {
					let productReview = {
						name: this.name,
						review: this.review,
						rating: this.rating
					}
	
					this.name = null;
					this.review = null;
					this.rating = null;

					this.$emit('submitReview', productReview);
				} else {
					!this.name && this.errors.push('Name required.');
					!this.review && this.errors.push('Review required.');
					!this.rating && this.errors.push('Rating required.');
				}
			}
		}
	}
</script>

<style scoped>
	form {
		width: 400px;
		border: 1px solid #d8d8d8;
		padding: 20px;
		margin: 40px;
	}

	input {
		width: 100%;  
		height: 25px;
		margin-bottom: 20px;
	}

	textarea {
		width: 100%;
		height: 60px;
	}
</style>