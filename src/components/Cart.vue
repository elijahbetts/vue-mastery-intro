<template>
	<div id="app">
		<div class="cart">
			<p>Cart ({{ cart.length }})</p>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'Cart',
		props: {
			cart: {
				type: Array,
				default: 0
			}
		}
	}
</script>

<style scoped>
	.cart {
		margin-right: 25px;
		float: right;
		border: 1px solid #d8d8d8;
		padding: 5px 20px;
	}
</style>