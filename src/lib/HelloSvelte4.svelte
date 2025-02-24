<script lang="ts">
	import { onMount, onDestroy, beforeUpdate, afterUpdate } from 'svelte';

	export let name;

	let count = 0;

	function increment() {
		count += 1;
	}

	$: console.log('sv4: count', count);

	// onMount: 컴포넌트가 DOM에 처음 마운트될 때 실행 (마운트 순서: 3번째)
	// - 외부 API 호출
	// - DOM 요소 조작
	// - 타이머/이벤트 리스너 설정
	// - SSR에서는 실행되지 않음
	onMount(() => {
		console.log('sv4: onMount');
	});

	// onDestroy: 컴포넌트가 제거되기 직전에 실행 (제거 시 실행)
	// - 타이머 정리
	// - 이벤트 리스너 제거
	// - 구독 취소
	// - 메모리 누수 방지를 위한 정리 작업
	onDestroy(() => {
		console.log('sv4: onDestroy');
	});

	// beforeUpdate: 컴포넌트가 업데이트되기 직전에 실행 (마운트/업데이트 순서: 2번째)
	// - DOM이 업데이트되기 전 현재 상태 저장
	// - 스크롤 위치 기억
	// - 반응성 구문($:) 실행 직후, DOM 업데이트 전에 호출
	beforeUpdate(() => {
		console.log('sv4: beforeUpdate');
	});

	// afterUpdate: 컴포넌트가 업데이트된 직후에 실행 (마운트 순서: 4번째, 업데이트 순서: 3번째)
	// - DOM 업데이트 후 추가 작업
	// - 스크롤 위치 복원
	// - 차트 등 외부 라이브러리 업데이트
	// - DOM이 실제로 변경된 후에 호출
	afterUpdate(() => {
		console.log('sv4: afterUpdate');
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
		{`Hello sv4: ${name}`}
	</div>

	<button
		class="rounded-lg border border-gray-200 bg-gray-100 px-4 py-2 text-gray-900 transition-all duration-200 hover:bg-gray-200"
		on:click={increment}
	>
		카운트: {count}
	</button>
</div>
