<script lang="ts">
	export let bg = 'white';
</script>

<div on:click on:keydown style="background-color: {bg};">
	<slot />
</div>

<style>
	div {
		width: 100%;
		height: 100%;
	}
</style>
