<script>
	import Counter from './Counter.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
	import wallet_img from '$lib/images/wallet.png';
	import Card from '$lib/components/Card.svelte';

</script>
<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<!-- <section>
	<h1>
		<span class="welcome">
			<picture>
				<source srcset={welcome} type="image/webp" />
				<img src={welcome_fallback} alt="Welcome" />
			</picture>
		</span>

		to your new<br />SvelteKit app
	</h1>

	<h2>
		try editing <strong>src/routes/+page.svelte</strong>
	</h2>

	<Counter />
</section> -->
<section>
	<div class="flex gap-3">
		<div class="w-[70%]">
			<div class="card">
				<div class="my-3">
					<h5 class="font-semibold">Wallet</h5>
				</div>
				<div>
					<img src={wallet_img}  alt="img"  width="100%">
				</div>
			</div>
		</div>
		<div class="w-[30%]">
			
			<div class="card">
				<div class="my-3">
					<h5 class="font-semibold">Wallet</h5>
				</div>
				<div>
					<p>Now here’s a cool one. Hover and the card’s contents slide away, making room for a fresh color and a logo. Smooth.</p>
				</div>
			</div>
		</div>
	</div>
	<div class="flex gap-3 mt-3">
		<div class="w-[30%]">
			<div class="card">
				<div class="my-3">
					<h5 class="font-semibold">Wallet</h5>
				</div>
				<div>
					<p>Now here’s a cool one. Hover and the card’s contents slide away, making room for a fresh color and a logo. Smooth.</p>
				</div>
			</div>
		</div>
		<div class="w-[70%]">
			<div class="card">
				<div class="my-3">
					<h5 class="font-semibold">Wallet</h5>
				</div>
				<div>
					<p>Now here’s a cool one. Hover and the card’s contents slide away, making room for a fresh color and a logo. Smooth.</p>
				</div>
			</div>
		</div>

	</div>
</section>
<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	.card {
    /* height: fit-content; */
		height: 100%;
    /* background: rgba(255, 255, 255, 0.2); */
    border: solid 1px rgba(255, 255, 255, 0.7);
    border-radius: 15px;
    padding: 2rem 2rem 1rem 2rem;
    box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.15);
    flex-direction: column;
    backdrop-filter: blur(20px);
    z-index: 100;
    transition: width 1s, height 350ms;
		background-image: linear-gradient(135deg, #ffffff, #f0f0f0, #ffffff);
  }
	.circle {
		width: 300px;
		height: 300px;
		border-radius: 50%;
		filter: blur(60px);
	}

	.circlebg {
		display: flex;
		position: absolute;
		z-index: -2;
		opacity: 0.7;
	}
	.circle-red {
		background: red;
		transform: translateX(40%);
	}
	.circle-blue {
		background-color: blue;
		transform: translateX(-40%);
	}
	.circle-green {
		background-color: green;
	}
	.circle-yellow {
		background-color: yellow;
		transform: translateX(-80%);
	}

</style>
