<script lang="ts">
	import Header from '$lib/header.svelte';

	import MagicBall from '$lib/magic-ball.svelte';
</script>

<Header />
<div class="page">
	<div class="fix center pattern">
		<MagicBall />
	</div>
</div>

<style>
	.pattern {
		background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24' viewBox='0 0 24 24'%3E%3Cg fill='%234a8dab' fill-opacity='0.4'%3E%3Cpath d='M12 20.485l8.485-8.485-8.485-8.485-8.485 8.485zM12 22l10-10-10-10-10 10z'/%3E%3C/g%3E%3C/svg%3E");
		background-size: 50px 50px;
	}

	.center {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.page {
		height: 300vh;
		width: 100vw;
		overflow: scroll;
	}
	.fix {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
	}
</style>
