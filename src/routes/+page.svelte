<script lang="ts">
	import Chessboard from '$lib/components/Chessboard.svelte';
	function handleClick(event: CustomEvent<{ row: number; col: number }>) {
		console.log('row', event.detail.row, 'col', event.detail.col);
	}
</script>

<Chessboard size="576px" rows={8} cols={8} on:click={handleClick} />
