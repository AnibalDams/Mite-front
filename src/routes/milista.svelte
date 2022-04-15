<script type="text/javascript">
	import MyListDesktop from '../components/desktop/pages/myList.svelte';
	import MyListMobile from '../components/mobileComponents/myList.svelte';
	let width;
</script>

<svelte:window bind:innerWidth={width} />

{#if width > 1020}
	<MyListDesktop />
{:else}
	<MyListMobile />
{/if}
