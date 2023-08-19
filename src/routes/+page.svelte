<script lang="ts">
	import { popup } from '@skeletonlabs/skeleton';
	import type { PopupSettings } from '@skeletonlabs/skeleton';
	import { toastStore } from '@skeletonlabs/skeleton';
	import type { ToastSettings } from '@skeletonlabs/skeleton';

	const popupFeatured: PopupSettings = {
		// Represents the type of event that opens/closed the popup
		event: 'click',
		// Matches the data-popup value on your popup element
		target: 'popupFeatured',
		// Defines which side of your trigger the popup will appear
		placement: 'top'
	};

	function handleClick(myString: string) {
		const t: ToastSettings = {
			message: `${myString}`
		};
		toastStore.trigger(t);
	}

	let searchedValue = '';

	let product = {
		name: 't-shirt',
		quantity: 0
	};

	function increment() {
		product.quantity += 1;
	}

	let products = [
		{
			name: 't-shirt',
			quantity: 20
		},
		{
			name: 'mug',
			quantity: 30
		},
		{
			name: 'sticker',
			quantity: 40
		},
		{
			name: 'sweatshirt',
			quantity: 50
		}
	];
</script>

{#if product.quantity > 10}
	<div class="variant-filled-primary p-4">
		<p>This product is in stock</p>
	</div>
{:else if product.quantity === 0}
	<div class="variant-filled-error p-4">
		<p>This product is out of stock</p>
	</div>
{:else}
	<div class="variant-filled-warning p-4">
		<p>Only a few items left</p>
	</div>
{/if}

<ul class="list">
	{#each products as product, i (product.name)}
		<li>
			<span class="flex-auto mb-10">
				<h3 class="h3">{product.name}</h3>
				<input type="checkbox" />
				<div>{i}</div>
			</span>
		</li>
	{/each}
</ul>

<div class="container h-full mx-auto flex justify-center items-center">
	<form action="" class="card p-4 flex flex-col gap-3">
		<h2 class="h2">Current {product.name} Quantity: {product.quantity}</h2>
		<button type="button" class="btn variant-filled-primary self-end" on:click={() => increment()}
			>Increment Quantity</button
		>

		<button class="btn variant-filled" use:popup={popupFeatured}>Show Popup</button>

		<div class="card p-4 variant-filled-primary" data-popup="popupFeatured">
			<p>Click Content</p>
			<div class="arrow variant-filled-primary" />
		</div>
		<button
			type="button"
			class="btn variant-filled-primary self-end"
			on:click={() => handleClick('This is the string')}>Show Toast</button
		>
		<h3 class="h3">Searched: {searchedValue}</h3>
		<input bind:value={searchedValue} class="input" type="text" id="myText" />
	</form>
</div>

<style lang="postcss">
</style>
