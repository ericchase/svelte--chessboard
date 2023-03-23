<script lang="ts">
	const FILE = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'] as const;
	type File = (typeof FILE)[number];
	const files: readonly File[] = FILE;
</script>

{#each files as file}
	<span>{file}</span>
{/each}
