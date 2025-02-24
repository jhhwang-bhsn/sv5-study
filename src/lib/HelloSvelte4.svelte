<script lang="ts">
	export let name;

	let count = 0;

	function increment() {
		count += 1;
	}
</script>

<div class="flex flex-1 items-center justify-between gap-2">
	<div>
		{`Hello sv4: ${name}`}
	</div>

	<button
		class="rounded-lg border border-gray-200 bg-gray-100 px-4 py-2 text-gray-900 transition-all duration-200 hover:bg-gray-200"
		on:click={increment}
	>
		카운트: {count}
	</button>
</div>
