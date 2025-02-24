<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	let { name } = $props();

	let count = $state(0);

	function increment() {
		count += 1;
	}

	// $effect.pre: 컴포넌트 업데이트 사이클의 첫 번째 단계
	// - DOM 업데이트 전 실행
	// - 현재 상태 저장이 필요한 경우 사용
	// - 이전 상태와 비교가 필요한 로직 처리
	$effect.pre(() => {
		console.log('sv5: $effect.pre(beforeUpdate)', count, $effect.tracking());
	});

	// $effect.root: $effect.pre 이후, $effect 이전에 실행
	// - DOM 업데이트 직후 실행
	// - 외부 라이브러리 연동
	// - DOM 기반 계산이 필요한 작업 수행
	$effect.root(() => {
		console.log('sv5: $effect.root', count, $effect.tracking());
		return function cleanUp() {
			console.log('sv5: $effect.root cleanUp');
		};
	});

	// $effect: $effect.root 이후, onMount 이전에 실행
	// - 반응형 상태 변화에 따른 부수 효과 처리
	// - 파생된 상태 계산
	// - 비동기 작업 처리
	$effect(() => {
		console.log('sv5: count', count, $effect.tracking());
	});

	// onMount: 초기 렌더링 사이클의 마지막 단계
	// - 컴포넌트가 완전히 마운트된 후 실행
	// - 초기 데이터 로딩
	// - 외부 API 연동 설정
	onMount(() => {
		console.log('sv5: onMount', $effect.tracking());
	});

	// onDestroy: 컴포넌트 제거 시 실행
	// - 리소스 정리
	// - 이벤트 리스너 제거
	// - 구독 취소
	onDestroy(() => {
		console.log('sv5: onDestroy', $effect.tracking());
	});
	// # sv4 lifecycle 순서
	// 마운트 시 각 라이프사이클 호출 순서
	// 반응성구문 -> beforeUpdate -> onMount -> afterUpdate

	// 상태 변경시 라이프사이클 호출 순서
	// 반응성구문 -> beforeUpdate -> afterUpdate

	// # sv5 lifecycle 순서
	// 마운트 시 각 라이프사이클 호출 순서
	// $effect.pre(beforeUpdate) -> $effect.root -> $effect -> onMount

	// 상태 변경시 라이프사이클 호출 순서
	// $effect.pre(beforeUpdate) -> $effect
</script>

<div class="flex flex-1 items-center justify-between gap-2">
	<div>
		{`Hello sv5: ${name}`}
	</div>

	<button
		class="rounded-lg border border-gray-200 bg-gray-100 px-4 py-2 text-gray-900 transition-all duration-200 hover:bg-gray-200"
		onclick={increment}
	>
		카운트: {count}
	</button>
</div>
