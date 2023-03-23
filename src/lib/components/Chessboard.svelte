<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	import QueenLight from '$lib/SVGs/QueenLight.svg';

	import Files from './Chessboard/Files.svelte';
	import Ranks from './Chessboard/Ranks.svelte';
	import Square from './Chessboard/Square.svelte';

	export let size = '576px';
	// export let rows = 8;
	// export let cols = 8;
	export let colors = {
		Piece: {
			Dark: '#38180B',
			Light: '#FFFFFF'
		},
		Square: {
			Dark: '#732E11',
			Light: '#FFEDE4'
		},
		Text: {
			Light: 'white'
		}
	};
	const style = `
        --piece-dark: ${colors.Piece.Dark};
        --piece-light: ${colors.Piece.Light};
        --square-dark: ${colors.Square.Dark};
        --square-light: ${colors.Square.Light};
        --text-light: ${colors.Text.Light};
        --square-size: calc(${size} / 9);
        --half-square-size: calc(var(--square-size) / 2);
    `;

	export let pieces: Map<string, string> = new Map([['0,0', QueenLight]]);

	function forwardClick(row: number, col: number) {
		dispatch('click', { row, col });
	}
</script>

<div class="board" {style}>
	<div class="file-row"><Files /></div>
	<div class="row">
		<div class="file-col"><Ranks /></div>
		<div class="col">
			{#each new Array(4) as _, row}
				<div class="square-row">
					{#each new Array(4) as _, col}
						{#each ['--square-light', '--square-dark'] as color, i}
							<Square bg="var({color})" on:click={() => forwardClick(2 * row, 2 * col + i)}>
								{#if pieces.has(`${2 * row},${2 * col + i}`)}
									<img src={pieces.get(`${2 * row},${2 * col + i}`)} alt="piece" />
								{/if}
							</Square>
						{/each}
					{/each}
				</div>
				<div class="square-row">
					{#each new Array(4) as _, col}
						{#each ['--square-dark', '--square-light'] as color, i}
							<Square bg="var({color})" on:click={() => forwardClick(2 * row + 1, 2 * col + i)}>
								{#if pieces.has(`${2 * row + 1},${2 * col + i}`)}
									<img src={pieces.get(`${2 * row + 1},${2 * col + i}`)} alt="piece" />
								{/if}
							</Square>
						{/each}
					{/each}
				</div>
			{/each}
		</div>
		<div class="file-col"><Ranks /></div>
	</div>
	<div class="file-row"><Files /></div>
</div>

<style>
	.board {
		background-color: var(--piece-dark);
		color: var(--text-light);
		font-size: calc(var(--square-size) * 0.35);
		width: calc(var(--square-size) * 9);
		height: calc(var(--square-size) * 9);
	}
	.row {
		display: flex;
		flex-direction: row;
	}
	.col {
		display: flex;
		flex-direction: column;
	}
	.file-row {
		display: grid;
		grid-template-columns: repeat(8, var(--square-size));
		align-content: flex-end;
		justify-items: center;
		height: var(--half-square-size);
		margin: 0 var(--half-square-size);
	}
	.file-col {
		display: grid;
		grid-template-rows: repeat(8, var(--square-size));
		align-items: center;
		justify-items: center;
		width: var(--half-square-size);
	}
	.square-row {
		display: flex;
		flex-direction: row;
		width: calc(var(--square-size) * 8);
		height: var(--square-size);
	}
</style>
