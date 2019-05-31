<template>
	<div id="app">
		<div class="nav-bar"></div>

		<div class="product">
			<div class="product-image">
				<img :src="image" />
			</div>
			<div class="product-info">
				<h1>{{ title }}</h1>
				<p v-if="inStock > 0">In Stock</p>
				<p v-else>Out of Stock</p>

				<ul>
					<li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
				</ul>

				<div v-for="(variant, index) in variants" :key="index" class="color-box" :class="variant.variantColor" @mouseover="updateProduct(index)"></div>

				<button @click="addToCart" :disabled="!inStock" :class="{ disabledButton: !inStock }">Add to Cart</button>

				<div class="cart">
					<p>Cart ({{ cart }})</p>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import greenSocks from '@/assets/vmSocks-green.jpg';
	import blueSocks from '@/assets/vmSocks-blue.jpg';

	export default {
		name: 'Socks',
		data() {
			return {
				brand: 'Vue Mastery',
				product: 'Socks',
				selectedVariant: 0,
				details: ['80% cotton', '20% polyester', 'Gender-neutral'],
				variants: [
					{
						variantId: 2234,
						variantColor: 'green',
						variantImage: greenSocks,
						variantQuantity: 10
					},
					{
						variantId: 2235,
						variantColor: 'blue',
						variantImage: blueSocks,
						variantQuantity: 0
					}
				],

				cart: 0
			}
		},
		methods: {
			addToCart() {
				this.cart += 1;
			},
			updateProduct(index) {
				this.selectedVariant = index;
			}
		},
		computed: {
			title() {
				return this.brand + ' ' + this.product;
			},
			image() {
				return this.variants[this.selectedVariant].variantImage;
			},
			inStock() {
				return this.variants[this.selectedVariant].variantQuantity;
			}
		}
	}
</script>

<style scoped>
	body {
		font-family: tahoma;
		color:#282828;
		margin: 0px;
	}

	.nav-bar {
		background: linear-gradient(-90deg, #84CF6A, #16C0B0);
		height: 60px;
		margin-bottom: 15px;
	}

	.product {
		display: flex;
		flex-flow: wrap;
		padding: 1rem;
	}

	img {
		border: 1px solid #d8d8d8;
		width: 70%;
		margin: 40px;
		box-shadow: 0px .5px 1px #d8d8d8;
	}

	.product-image {
		width: 80%;
	}

	.product-image,
	.product-info {
		margin-top: 10px;
		width: 50%;
	}

	.color-box {
		width: 40px;
		height: 40px;
		margin-top: 5px;
	}

	.color-box.green {
		background-color: green;
	}

	.color-box.blue {
		background-color: blue;
	}

	.cart {
		margin-right: 25px;
		float: right;
		border: 1px solid #d8d8d8;
		padding: 5px 20px;
	}

	button {
		margin-top: 30px;
		border: none;
		background-color: #1E95EA;
		color: white;
		height: 40px;
		width: 100px;
		font-size: 14px;
	} 

	.disabledButton {
		background-color: #d8d8d8;
	}

	.review-form {
		width: 400px;
		padding: 20px;
		margin: 40px;
		border: 1px solid #d8d8d8;
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

	.tab {
		margin-left: 20px;
		cursor: pointer;
	}

	.activeTab {
		color: #16C0B0;
		text-decoration: underline;
	}
</style>