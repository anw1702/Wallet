

<script>
	/**
   * @type {boolean}
   */
	 export let showModal; // boolean

	/**
   * @type {HTMLDialogElement}
   */
	let dialog; // HTMLDialogElement

	$: if (dialog && showModal) dialog.showModal();
</script>

<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-noninteractive-element-interactions -->
<dialog
	bind:this={dialog}
	on:close={() => (showModal = false)}
	on:click|self={() => dialog.close()}
>
	<!-- svelte-ignore a11y-no-static-element-interactions -->
	<div on:click|stopPropagation>
		<slot name="header" />
		<hr />
		<slot />
		<hr />
		<!-- svelte-ignore a11y-autofocus -->
		
	</div>
</dialog>

<style>
	dialog {
		max-width: 36em;
		border-radius: 0.5m;
		border: none;
		padding: 0;
	}
	dialog::backdrop {
		background: rgba(0, 0, 0, 0.426);
	}
	dialog > div {
		padding: 1em;
	}
	dialog[open] {
		animation: forwards 1 cubic-bezier(0.34, 1.56, 0.64, 1);
	}
	@keyframes forwards {
		from {
			transform: scale(0.95);
		}
		to {
			transform: scale(1);
		}
	}
	dialog[open]::backdrop {
		animation:normal cubic-bezier(0.075, 0.82, 0.165, 1);
	}
	@keyframes normal {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
</style>