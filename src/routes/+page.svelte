<script lang="ts">
	import MetafoldMark from '$lib/components/MetafoldMark.svelte';

	const WORDMARK = 'METAFOLD';
</script>

<div class="page">
	<div class="ambient" aria-hidden="true"></div>
	<div class="kerf" aria-hidden="true"></div>
	<div class="grain" aria-hidden="true"></div>

	<main>
		<div class="mark-wrap">
			<MetafoldMark />
		</div>

		<h1 class="wordmark" aria-label={WORDMARK}>
			{#each WORDMARK as letter, i (i)}
				<span aria-hidden="true" style="--i: {i}">{letter}</span>
			{/each}
		</h1>

		<p class="status">
			LAUNCHING SOON<span class="cursor" aria-hidden="true"></span>
		</p>

		<p class="sub">Precision laser-cut MDF · Made in India</p>
	</main>

	<footer>
		<!-- PLACEHOLDER_WHATSAPP_NUMBER still needs the real number (country code, no +). -->
		<a href="https://wa.me/PLACEHOLDER_WHATSAPP_NUMBER">Enquiries</a>
		<span aria-hidden="true">·</span>
		<a href="mailto:hello@metafold.co.in">hello@metafold.co.in</a>
	</footer>
</div>

<style>
	@font-face {
		font-family: 'Space Grotesk';
		font-style: normal;
		font-weight: 300 700;
		font-display: swap;
		src: url('/fonts/space-grotesk-latin.woff2') format('woff2');
	}

	/* keeps mobile overscroll and scrollbars from flashing white behind the canvas */
	:global(html) {
		background: #0b0a09;
		color-scheme: dark;
	}

	/* ponytail: custom props live on .page, not :root — the whole unit deletes with one file. */
	.page {
		--canvas: #0b0a09;
		--logo: #f5f0e8;
		--laser: #ff7a18;
		--laser-core: #ffe9c4;
		--muted: #8a8175;

		position: relative;
		display: flex;
		min-height: 100dvh;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: clamp(2rem, 8vh, 4rem);
		overflow: hidden;
		padding: clamp(1.5rem, 5vw, 3rem);
		background: var(--canvas);
		color: var(--logo);
		font-family: 'Space Grotesk', ui-sans-serif, system-ui, sans-serif;
		text-align: center;
	}

	/* Ambient drift, kerf grid and grain are decoration and never take a click. */
	.ambient,
	.kerf,
	.grain {
		position: absolute;
		inset: 0;
		pointer-events: none;
	}

	.ambient {
		inset: -20%;
		background: radial-gradient(
			42% 42% at 50% 42%,
			rgba(255, 122, 24, 0.16) 0%,
			rgba(255, 122, 24, 0.05) 40%,
			transparent 72%
		);
		animation: drift 20s ease-in-out infinite alternate;
	}

	.kerf {
		opacity: 0.04;
		background-image:
			linear-gradient(to right, var(--logo) 1px, transparent 1px),
			linear-gradient(to bottom, var(--logo) 1px, transparent 1px);
		background-size: 48px 48px;
		mask-image: radial-gradient(70% 70% at 50% 50%, #000 30%, transparent 100%);
		animation: fade-in 0.9s ease-out both;
	}

	.grain {
		opacity: 0.03;
		background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
	}

	main {
		position: relative;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: clamp(1.25rem, 4vh, 2rem);
	}

	.mark-wrap {
		width: min(280px, 62vw);
		animation: settle 1.1s ease-out 1.6s both;
	}

	.wordmark {
		margin: 0;
		font-size: clamp(1.75rem, 9vw, 3.25rem);
		font-weight: 600;
		line-height: 1;
		letter-spacing: 0.22em;
		/* letter-spacing pads the right edge; nudge back to optical centre */
		text-indent: 0.22em;
	}

	.wordmark span {
		display: inline-block;
		opacity: 1;
		animation: rise 0.5s ease-out calc(2.2s + var(--i) * 30ms) both;
	}

	.status {
		margin: 0;
		font-family: ui-monospace, 'SFMono-Regular', Menlo, Consolas, monospace;
		font-size: clamp(0.75rem, 3.2vw, 0.875rem);
		font-weight: 500;
		letter-spacing: 0.42em;
		text-indent: 0.42em;
		color: var(--laser);
		opacity: 1;
		animation: rise 0.5s ease-out 2.6s both;
	}

	.cursor {
		display: inline-block;
		width: 0.5em;
		height: 1em;
		margin-left: 0.1em;
		background: currentColor;
		vertical-align: -0.12em;
		animation: blink 1.1s steps(1, end) 3.1s infinite;
	}

	.sub {
		margin: 0;
		max-width: 34ch;
		font-size: clamp(0.8125rem, 3.4vw, 0.9375rem);
		color: var(--muted);
		opacity: 1;
		animation: rise 0.6s ease-out 2.9s both;
	}

	footer {
		position: absolute;
		bottom: clamp(1.25rem, 4vh, 2.5rem);
		left: 1rem;
		right: 1rem;
		display: flex;
		flex-wrap: wrap;
		align-items: center;
		justify-content: center;
		gap: 0.75rem;
		font-size: 0.8125rem;
		color: var(--muted);
		opacity: 1;
		animation: rise 0.6s ease-out 3.1s both;
	}

	footer a {
		padding-bottom: 2px;
		border-bottom: 1px solid rgba(138, 129, 117, 0.4);
		color: var(--muted);
		text-decoration: none;
		transition: color 0.2s ease;
	}

	footer a:hover,
	footer a:focus-visible {
		color: var(--logo);
	}

	@keyframes fade-in {
		from {
			opacity: 0;
		}
	}

	/* ponytail: 0.001 rather than 0 — Chrome drops an element from LCP consideration
	   if it is opacity:0 on first paint and never reconsiders it, so a fade-in intro
	   leaves the page with no LCP at all. Visually identical, metric stays measurable. */
	@keyframes rise {
		from {
			opacity: 0.001;
			transform: translateY(6px);
		}
	}

	@keyframes settle {
		from {
			transform: scale(0.98);
		}
	}

	@keyframes drift {
		from {
			transform: translate3d(-3%, -2%, 0) scale(1);
		}
		to {
			transform: translate3d(3%, 2%, 0) scale(1.12);
		}
	}

	@keyframes blink {
		0%,
		49% {
			opacity: 1;
		}
		50%,
		100% {
			opacity: 0;
		}
	}

	@media (min-width: 768px) {
		.mark-wrap {
			width: min(420px, 34vw);
		}
	}

	/* Base styles above are already the composed end state, so switching motion off
	   is literally "stop animating" — nothing to restore. */
	@media (prefers-reduced-motion: reduce) {
		.ambient,
		.kerf,
		.mark-wrap,
		.wordmark span,
		.status,
		.cursor,
		.sub,
		footer {
			animation: none;
		}
	}
</style>
