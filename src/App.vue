<template>
	<div id="app">
		<div class="nav-bar"></div>
		<Cart :cart="cart" />
		<Socks :premium="premium" @updateCart="updateCart" />
	</div>
</template>

<script>
	import Cart from './components/Cart.vue';
	import Socks from './components/Socks.vue';

	export default {
		name: 'app',
		components: {
			Cart, Socks
		},
		data() {
			return {
				premium: true,
				cart: []
			}
		},
		methods: {
			updateCart(id) {
				this.cart.push(id);
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
