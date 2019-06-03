<template>
	<div id="app">
		<div class="product">
			<div class="product-image">
				<img :src="image" />
			</div>
			<div class="product-info">
				<h1>{{ title }}</h1>
				<p v-if="inStock > 0">In Stock</p>
				<p v-else>Out of Stock</p>
				<p>Shipping: {{ shipping }}</p>

				<ul>
					<li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
				</ul>

				<div v-for="(variant, index) in variants" :key="index" class="color-box" :class="variant.variantColor" @mouseover="updateProduct(index)"></div>

				<button @click="addToCart" :disabled="!inStock" :class="{ disabledButton: !inStock }">Add to Cart</button>
			</div>
			<div class="product-reviews">
				<h2>Reviews</h2>
				<p v-if="!reviews.length">There are no reviews yet.</p>
				
				<ul>
					<li v-for="review in reviews">
						<p>{{ review.name }}</p>
						<p>Rating: {{ review.rating }}</p>
						<p>{{ review.review }}</p>
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
	import greenSocks from '@/assets/vmSocks-green.jpg';
	import blueSocks from '@/assets/vmSocks-blue.jpg';

	export default {
		name: 'Socks',
		props: {
			premium: {
				type: Boolean,
				required: true
			},
			reviews: {
				type: Array,
				required: true
			}
		},
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
				]
			}
		},
		methods: {
			addToCart() {
				this.$emit('updateCart', this.variants[this.selectedVariant].variantId);
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
			},
			shipping() {
				return this.premium ? 'Free' : '$2.99';
			}
		}
	}
</script>

<style scoped>
	.product {
		display: flex;
		flex-flow: wrap;
		padding: 1rem;
	}

	.product-image {
		width: 80%;
	}

	.product-image img {
		width: 70%;
		border: 1px solid #d8d8d8;
		box-shadow: 0px .5px 1px #d8d8d8;
		margin: 40px;
	}

	.product-image,
	.product-info {
		width: 50%;
		margin-top: 10px;
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

	button {
		width: 100px;
		height: 40px;
		font-size: 14px;
		color: #ffffff;
		border: none;
		background-color: #1E95EA;
		margin-top: 30px;
		cursor: pointer;
	} 

	.disabledButton {
		background-color: #d8d8d8;
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