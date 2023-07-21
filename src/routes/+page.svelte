<script lang="ts">
	let panelStyle = '';

	// const degreesFromPercent = (percent: number): string => `${(90 * percent) / 100}deg`;
	// const positionFromPercent = (percent: number): string => `calc(${(35 * percent) / 100}vmin)`;

	function onScroll() {
		const { scrollTop, scrollHeight, clientHeight } = document.documentElement;
		const maxScrollTop = scrollHeight - clientHeight;
		const percent = scrollTop / maxScrollTop;
		document.documentElement.style.setProperty('--frame', percent.toString());

		/*
		panelStyle = [
			'transform-style: preserve-3d; perspective:500px; perspective-origin: center;',
			'transform:',
			'translateZ(-10vmin)',
			//'translate(-50%,-50%)',
			`rotateX(${degreesFromPercent(percent)})`,
			//`translateZ(${positionFromPercent(percent)})`,
			//`rotate3D(1, 0, 0, ${degreesFromPercent(percent)}deg)`,
			//`translateY(${positionFromPercent(percent)});`
			';'
		].join(' ');
		*/
	}
</script>

<header>
	<h1>8 ball</h1>
</header>
<svelte:window on:scroll={onScroll} />

<div class="page">
	<div class="fix center pattern">
		<figure class="ball center">
			<div class="panels scroll-animated">
				<div class="number-panel center" style={panelStyle}>8</div>
				<div class="back-panel center">bla</div>
			</div>
		</figure>
	</div>
</div>

<style>
	:root {
		--size: 70vmin;
		--panel-size: 35vmin;
		background-color: #a0a0a0;
		--frame: 0.5;
	}

	.scroll-animated {
		/* Pause the animation */
		animation-play-state: paused;
		/* Bind the animation to scroll */
		animation-delay: calc(var(--frame) * -1s);
		/* These last 2 properites clean up overshoot weirdness */
		animation-iteration-count: 1;
		animation-fill-mode: both;
		animation-duration: 1s;
		transform-style: preserve-3d;
	}

	.pattern {
		background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24' viewBox='0 0 24 24'%3E%3Cg fill='%234a8dab' fill-opacity='0.4'%3E%3Cpath d='M12 20.485l8.485-8.485-8.485-8.485-8.485 8.485zM12 22l10-10-10-10-10 10z'/%3E%3C/g%3E%3C/svg%3E");
		background-size: 50px 50px;
	}

	header {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		z-index: 1;
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

	.ball {
		width: var(--size);
		aspect-ratio: 1;
		background-color: black;
		box-shadow: inset -1vmin 0vmin 4vmin rgba(255, 255, 255, 0.2), 0 4vmin 8vmin rgba(0, 0, 0, 0.5);
		background-image: linear-gradient(-45deg, rgba(255, 255, 220, 0.3) 0%, transparent 100%);

		border-radius: 50%;
		overflow: hidden;
	}

	@keyframes rotate-center-up {
		0% {
			opacity: 1;
			transform: perspective(300vmin) rotateX(0deg);
		}
		49% {
			opacity: 1;
			transform: perspective(1000vmin) scaleY(1.5) translateY(-40vmin) rotateX(120deg);
		}
		50% {
			opacity: 0;
			transform: perspective(1000vmin) translateY(-36vmin) rotateX(90deg);
		}
		100% {
			opacity: 0;
		}
	}
	.panels {
		width: var(--panel-size);
		height: var(--panel-size);
		transform-style: preserve-3d;
		animation-name: rotate-center-up;
		animation-timing-function: linear;
	}
	.panels > div {
		position: absolute;
	}
	.number-panel {
		transform: translateZ(100vmin);
		width: var(--panel-size);
		height: var(--panel-size);
		border-radius: 50%;
		background-color: white;
		color: black;
		font-family: sans-serif;
		font-size: var(--panel-size);
	}
	.back-panel {
		display:none;
		transform: translateZ(-100vmin) rotateZ(180deg);
		width: var(--panel-size);
		height: var(--panel-size);
		border-radius: 50%;
		background-color: white;
		color: black;
		font-family: sans-serif;
		font-size: var(--panel-size);
	}
</style>
