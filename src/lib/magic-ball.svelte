<script lang="ts">
	const THRESHOLD = 0.3;
	const answers = [
		'It is certain.',
		'It is decidedly so.',
		'Without a doubt.',
		'Yes – definitely.',
		'You may rely on it.',
		'As I see it, yes.',
		'Most likely.',
		'Outlook good.',
		'Yes.',
		'Signs point to yes.',
		'Reply hazy, try again.',
		'Ask again later.',
		'Better not tell you now.',
		'Cannot predict now.',
		'Concentrate and ask again.',
		"Don't count on it.",
		'My reply is no.',
		'My sources say no.',
		'Outlook not so good.',
		'Very doubtful.'
	];

	let answerIndex = 0;

	$: answer = answers[answerIndex];
	let point: 'up' | 'down' = 'up';

	function updateAnswer() {
		answerIndex = Math.floor(Math.random() * answers.length);
		point = Math.random() > 0.5 ? 'up' : 'down';
	}

	let prevPercent = 0;

	function onScroll() {
		const { scrollTop, scrollHeight, clientHeight } = document.documentElement;
		const maxScrollTop = scrollHeight - clientHeight;
		const percent = scrollTop / maxScrollTop;
		document.documentElement.style.setProperty('--frame', percent.toString());

		if (prevPercent < THRESHOLD && percent > THRESHOLD) {
			updateAnswer();
		}
		prevPercent = percent;
	}
</script>

<svelte:window on:scroll={onScroll} />

<figure class="ball center">
	<span class="stage-shadow" />
	<div class="panels scroll-animated">
		<div class="number-panel center scroll-animated front">8</div>
		<div class="back-panel center scroll-animated back">
			<div class={'answer ' + point}>{answer}</div>
		</div>
	</div>
</figure>

<style>
	:root {
		--size: 70vmin;
		--panel-size: 35vmin;
		background-color: #a0a0a0;
		--frame: 0;
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
	}

	.center {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.ball {
		position: relative;
		background: radial-gradient(circle at 50% 120%, #323232, #0a0a0a 80%, #000000 100%);
		width: var(--size);
		aspect-ratio: 1;
		box-shadow: inset -1vmin 0vmin 4vmin rgba(255, 255, 255, 0.2), 0 4vmin 8vmin rgba(0, 0, 0, 0.8);

		border-radius: 50%;
		overflow: hidden;
	}
	.ball:before {
		content: '';
		position: absolute;
		background: radial-gradient(
			circle at 50% 120%,
			rgba(255, 255, 255, 0.5),
			rgba(255, 255, 255, 0) 70%
		);
		border-radius: 50%;
		bottom: 2.5%;
		left: 5%;
		opacity: 0.3;
		height: 100%;
		width: 90%;
		filter: blur(2vmin);
		z-index: 2;
	}
	.ball:after {
		width: 100%;
		height: 100%;
		content: '';
		position: absolute;
		top: 5%;
		left: 10%;
		border-radius: 50%;
		background: radial-gradient(
			circle at 50% 50%,
			rgba(255, 255, 255, 0.8),
			rgba(255, 255, 255, 0.8) 14%,
			rgba(255, 255, 255, 0) 24%
		);
		opacity: 0.5;
		transform: translateX(-20vmin) translateY(-24vmin) skewX(-20deg);
		filter: blur(4vmin);
	}
	.stage-shadow {
		position: absolute;
		z-index: 1;
		top: 0;
		left: 0;
		width: var(--size);
		height: var(--size);
		background: radial-gradient(
			circle at 50% 50%,
			rgba(0, 0, 0, 0.4),
			rgba(0, 0, 0, 0.1) 40%,
			rgba(0, 0, 0, 0) 50%
		);
	}

	@keyframes ball-flip {
		from {
			transform: rotateX(0deg);
		}
		to {
			transform: rotateX(180deg);
		}
	}
	.panels {
		width: var(--panel-size);
		height: var(--panel-size);

		transform-style: preserve-3d;
		animation-name: ball-flip;
		transform: rotateX(0deg);
		perspective-origin: center;
	}
	.panels > div {
		position: absolute;
		top: 0;
		left: 0;
	}
	@keyframes front {
		0% {
			opacity: 1;
		}
		29% {
			opacity: 1;
		}
		30% {
			opacity: 0;
		}
		100% {
			opacity: 0;
		}
	}
	@keyframes back {
		0% {
			opacity: 0;
		}
		29% {
			opacity: 0;
		}
		30% {
			opacity: 1;
		}
		100% {
			opacity: 1;
		}
	}
	.front {
		opacity: 1;
		animation-name: front;
		transform: translateZ(35vmin);
	}
	.back {
		animation-name: back;
		transform: translateZ(-35vmin) rotateX(180deg);
	}

	.number-panel {
		width: var(--panel-size);
		height: var(--panel-size);
		border-radius: 50%;
		background-color: white;
		color: black;
		font-family: sans-serif;
		font-size: var(--panel-size);
		text-shadow: 0 0.2vmin 0.2vmin black;
		box-shadow: inset 0 0.2vmin 0.2vmin black;
	}
	.back-panel {
		width: var(--panel-size);
		height: var(--panel-size);
		border-radius: 50%;
		background-color: black;
		border: 0.2vmin solid rgba(200, 200, 200, 0.2);

		font-family: sans-serif;
		font-size: var(--panel-size);
		z-index: 10000;
		overflow: hidden;
	}
	.answer {
		position: relative;
		justify-content: center;
		align-items: center;
		display: flex;
		width: 18vmin;
		height: 20.8vmin;
		color: white;
		text-align: center;
		font-family: sans-serif;
		font-variant: small-caps;
		font-size: 2.1vmin;
		line-height: 2.4vmin;
		transition: opacity 1s;
		animation: floating 6s linear infinite;
	}

	/* Triangle */
	.answer::before {
		content: '';
		z-index: -1;
		position: absolute;
		left: 0;
		border-left: 8.8vmin solid transparent;
		border-right: 8.8vmin solid transparent;
		border-radius: 0.4vmin;
		width: 0.4vmin;
		height: 0;
	}

	.answer.up::before {
		top: 0.4vmin;
		border-bottom: 15.2vmin solid #1c23e8;
	}

	.answer.down::before {
		bottom: 0.4vmin;
		border-top: 15.2vmin solid #1c23e8;
	}

	/* Overlay */
	.answer::after {
		content: '';
		z-index: 100;
		position: absolute;
		left: -7vmin;
		top: -5vmin;
		border-radius: 50%;
		width: 32vmin;
		height: 32vmin;
		background: linear-gradient(to left, rgba(0, 0, 0, 0.9), rgba(0, 0, 0, 0));
		animation: rotating 6s infinite linear;
	}
	/* Triangle gently floating around */
	@keyframes floating {
		from {
			transform: rotateZ(0) rotateY(15deg) translateZ(6.8vmin) rotateZ(0);
		}
		to {
			transform: rotateZ(1turn) rotateY(15deg) translateZ(6.8vmin) rotateZ(-1turn);
		}
	}
	@keyframes rotating {
		to {
			transform: rotate(1turn);
		}
	}
</style>
