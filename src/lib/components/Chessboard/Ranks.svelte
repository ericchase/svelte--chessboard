<script lang="ts">
	const RANK = [1, 2, 3, 4, 5, 6, 7, 8] as const;
	type Rank = (typeof RANK)[number];
	const ranks: readonly Rank[] = RANK;
</script>

{#each ranks as rank}
	<span>{rank}</span>
{/each}
