<script lang="ts">
	import { onMount } from 'svelte';
	import productDesktop from '$lib/images/image-product-desktop.jpg';
	import productMobile from '$lib/images/image-product-mobile.jpg';

	import { IconShoppingCart } from '@tabler/icons-svelte';

	export let title: string;
	
	let isMobile: boolean;

	onMount(() => {
		function handleResize() {
			isMobile = window.innerWidth <= 375;
		}

		window.addEventListener('resize', handleResize);

		return () => {
			window.removeEventListener('resize', handleResize);
		};
	});
</script>

<div>
	<div id="flex">
		<div class="box1">
			{#if isMobile}
				<img src={productMobile} alt="Product chanel parfume" class="mobile-img" />
			{:else}
				<img src={productDesktop} alt="Product chanel parfume" />
			{/if}
		</div>
		<div class="box2">
			<span class="category">Perfume</span>
			<h1>{title}</h1>
			<p class="description">
				A floral, solar and voluptuous interpretation composed by Olivier Polge, Perfumer-Creator
				for the House of CHANEL.
			</p>
			<p class="price">$149.99 <span class="discount-price">$169.99</span></p>
			<button class="btn text-center"><IconShoppingCart /> Add to Cart</button>
		</div>
	</div>
</div>

<style lang="scss">
	@import '../../sass/abstracts/variables';

	#flex {
		display: flex;
		justify-content: center;
		align-items: center;
		background: $White;

		border-radius: 15px;

		position: absolute;
		top: 50%;
		left: 50%;

		transform: translate(-50%, -50%);
		max-width: 680px;
		gap: 35px;

		@media screen and (max-width: 375px) {
			flex-direction: column;
			width: 360px;
		}
	}

	.box1 {
		line-height: 0;
	}

	.box1 img {
		max-height: 500px;
		border-radius: 15px 0 0 15px;

		&.mobile-img {
			width: 100%;
			height: 100%;
			border-radius: 15px 15px 0 0;
		}
	}

	.box2 {
		color: $Dark;
		padding: 0 32px 0 0;

		@media screen and (max-width: 375px) {
			padding: 0 10px 0 20px;
			width: 100%;
		}

		h1 {
			margin: 25px 0;
			color: $Very;

			font-family: 'Fraunces', serif;
			font-weight: 700;

			font-size: 38px;
			line-height: 38px;
		}

		.category {
			text-transform: uppercase;
			font-size: 14px;
			letter-spacing: 5px;
		}

		.description {
			line-height: 25px;
			margin: 25px 0;
		}

		.btn {
			display: flex;
			align-items: center;
			justify-content: center;
			gap: 10px;

			color: $White;
			font-weight: 700;
			font-size: 16px;
			background: $DarkGreen;

			padding: 16px 0;
			width: 100%;
			border-radius: 10px;
			border: none;

			@media screen and (max-width: 375px) {
				margin-bottom: 20px;
			}
		}

		.price {
			margin: 25px 0;
			position: relative;

			color: $DarkGreen;
			font-family: 'Fraunces', serif;

			font-size: 35px;
			font-weight: 700;

			.discount-price {
				color: $Dark;

				font-family: 'Montserrat', sans-serif;
				font-weight: 500;
				text-decoration: line-through;

				font-size: 14px;
				top: 12px;
				right: 60px;
				position: absolute;

				@media screen and (max-width: 375px) {
					right: 115px;
				}
			}
		}
	}
</style>
