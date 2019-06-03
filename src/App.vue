<template>
	<div id="app">
		<div class="nav-bar"></div>
		<Cart :cart="cart" />
		<Socks :premium="premium" :reviews="reviews" @updateCart="updateCart" />
		<Review @submitReview="submitReview" />
	</div>
</template>

<script>
	import Cart from './components/Cart.vue';
	import Socks from './components/Socks.vue';
	import Review from './components/Review.vue';

	export default {
		name: 'app',
		components: {
			Cart, Socks, Review
		},
		data() {
			return {
				premium: true,
				cart: [],
				reviews: []
			}
		},
		methods: {
			updateCart(id) {
				this.cart.push(id);
			},
			submitReview(review) {
				this.reviews.push(review);
			}
		}
	}
</script>

<style>
	body {
		font-family: Tahoma;
		color: #282828;
		margin: 0px;
	}

	.nav-bar {
		background: linear-gradient(-90deg, #84CF6A, #16C0B0);
		height: 60px;
		margin-bottom: 15px;
	}
</style>
