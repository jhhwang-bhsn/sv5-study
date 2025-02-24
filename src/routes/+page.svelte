<script>
	import HelloSvelte4 from '$lib/HelloSvelte4.svelte';
	import HelloSvelte5 from '$lib/HelloSvelte5.svelte';
	let name = $state('Student1');
	import { onMount, onDestroy } from 'svelte';

	$effect.pre(() => {
		console.log('page: $effect.pre(beforeUpdate)');
	});

	$effect.root(() => {
		console.log('page: $effect.root');
		return function cleanUp() {
			console.log('page: $effect.root cleanUp');
		};
	});

	$effect(() => {
		console.log('page: name 변경', name);
	});

	onMount(() => {
		console.log('page: onMount');
	});

	onDestroy(() => {
		console.log('page: onDestroy');
	});
</script>

<div class="flex min-h-screen flex-col items-center justify-center bg-gray-100">
	<div class="w-full max-w-md rounded-lg bg-white p-8">
		<h1 class="mb-8 text-center text-2xl font-bold">Svelte 4 5 비교 및 테스트</h1>

		<div class="space-y-6">
			<div class="flex flex-col gap-2">
				<HelloSvelte4 {name} />
				<HelloSvelte5 {name} />
			</div>

			<div class="space-y-2">
				<label class="text-gray-600">이름</label>
				<input
					type="text"
					bind:value={name}
					class="w-full rounded-lg border border-gray-200 px-4 py-3 text-base transition-all hover:border-gray-300 focus:border-blue-500 focus:ring-2 focus:ring-blue-100 focus:outline-none"
					placeholder="이름을 입력하세요"
				/>
			</div>
		</div>

		<div class="mt-6 space-y-4">
			<h2 class="text-lg font-semibold">독립적 사용</h2>
			<p class="text-gray-600">
				Svelte 5의 새로운 rune 문법과 Svelte 4의 기존 문법은 각각의 컴포넌트에서 독립적으로 사용
				가능합니다. 서로 다른 컴포넌트에서는 각각의 문법을 자유롭게 선택하여 사용할 수 있습니다.
			</p>

			<h2 class="text-lg font-semibold">제한사항</h2>
			<p class="text-gray-600">
				Svelte 5 문법을 사용하는 컴포넌트 내에서는 Svelte 4의 문법을 함께 사용할 수 없습니다. 두
				문법은 상호 배타적입니다.
			</p>
		</div>
	</div>
</div>
