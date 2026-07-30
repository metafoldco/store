<!--
	Metafold mark. The source paths are closed FILL outlines, so the laser trace is a
	second, stroked copy of the same geometry via <use> — no dash animation ever touches
	a filled path. pathLength="1" lets the dash maths stay in 0..1 with no JS measuring.
-->
<svg
	class="mark"
	viewBox="0 0 1290.000000 1290.000000"
	preserveAspectRatio="xMidYMid meet"
	role="img"
	aria-label="Metafold"
>
	<defs>
		<path
			id="mf-p1"
			pathLength="1"
			d="M2586 9533 c-13 -7 -34 -28 -45 -47 l-21 -34 2 -3053 3 -3054 22 -47
c42 -92 126 -161 228 -187 160 -42 336 55 389 213 15 46 16 211 16 1892 0
1253 3 1851 11 1871 27 78 128 117 194 75 28 -18 200 -294 745 -1192 249 -410
804 -1317 819 -1337 39 -53 140 -57 192 -7 16 15 29 31 29 35 0 4 128 211 284
461 156 249 712 1139 1235 1977 524 838 957 1530 964 1537 7 7 28 34 47 59 41
54 140 122 225 156 l60 24 1290 5 c710 3 1299 9 1310 13 144 61 212 146 231
288 15 110 -45 238 -146 308 -30 21 -67 41 -82 45 -14 3 -687 6 -1495 6 -1533
1 -1490 2 -1583 -36 -3 -1 -15 -5 -27 -9 -13 -4 -23 -11 -23 -15 0 -5 -9 -12
-20 -15 -28 -9 -133 -113 -156 -155 -10 -19 -21 -37 -24 -40 -3 -3 -28 -41
-54 -85 -27 -44 -81 -129 -121 -190 -40 -60 -79 -123 -88 -140 -9 -16 -24 -45
-33 -62 -10 -18 -21 -33 -26 -33 -4 0 -8 -7 -8 -15 0 -8 -4 -15 -9 -15 -5 0
-11 -8 -15 -17 -6 -19 -27 -55 -37 -63 -3 -3 -13 -19 -22 -36 -9 -18 -64 -108
-123 -200 -59 -93 -128 -203 -154 -244 -25 -41 -79 -127 -119 -190 -39 -63
-77 -124 -84 -134 -36 -58 -122 -196 -142 -226 -12 -19 -114 -181 -225 -360
-112 -179 -211 -336 -221 -350 -16 -24 -253 -403 -274 -438 -5 -9 -77 -123
-158 -252 -81 -129 -153 -244 -160 -254 -27 -44 -54 -69 -94 -88 -35 -17 -48
-18 -75 -9 -66 23 -7 -67 -658 1001 -699 1146 -933 1528 -1190 1950 -123 201
-261 428 -307 505 -115 191 -124 203 -153 211 -41 12 -97 11 -124 -3z"
		/>
		<path
			id="mf-p2"
			pathLength="1"
			d="M7516 7293 c-1 -1 -15 -4 -32 -7 -82 -15 -178 -96 -220 -188 l-29
-63 0 -1840 0 -1840 28 -57 c71 -144 229 -224 374 -189 138 33 227 125 253
258 8 42 10 566 8 1868 l-3 1810 -22 47 c-42 92 -140 173 -233 193 -32 7 -119
13 -124 8z"
		/>
		<path
			id="mf-p3"
			pathLength="1"
			d="M8700 7161 c-8 -6 -17 -8 -21 -5 -4 2 -36 -10 -70 -28 -126 -65 -191
-166 -192 -299 -1 -67 4 -86 32 -143 32 -65 95 -131 153 -160 71 -36 117 -37
1048 -34 l915 3 59 29 c132 65 209 202 191 341 -8 70 -56 165 -103 206 -35 31
-126 79 -167 88 -41 9 -1830 11 -1845 2z"
		/>
	</defs>
	<g
		transform="translate(0.000000,1290.000000) scale(0.100000,-0.100000)"
		fill="currentColor"
		stroke="none"
	>
		<g class="solid">
			<use href="#mf-p1" />
			<use href="#mf-p2" />
			<use href="#mf-p3" />
		</g>
		<g
			class="trace"
			fill="none"
			stroke="currentColor"
			stroke-width="60"
			stroke-linejoin="round"
			stroke-linecap="round"
		>
			<use href="#mf-p1" style="--d: 0.30s" />
			<use href="#mf-p2" style="--d: 0.48s" />
			<use href="#mf-p3" style="--d: 0.66s" />
		</g>
	</g>
</svg>

<style>
	.mark {
		display: block;
		width: 100%;
		height: auto;
		color: var(--logo);
	}

	/* Base styles are the FINAL state; keyframes only define where things come FROM.
	   That way killing animations (reduced motion) lands on the composed page. */
	.solid {
		opacity: 1;
		animation:
			fill-in 1.1s ease-out 1.6s both,
			scorch 1.8s ease-out 1.6s both;
	}

	.trace {
		opacity: 0;
		color: var(--laser-core);
		filter: drop-shadow(0 0 8px rgba(255, 122, 24, 0.75));
		animation: trace-out 0.6s ease-out 1.95s both;
	}

	.trace use {
		stroke-dasharray: 1;
		stroke-dashoffset: 0;
		animation: draw 1.35s cubic-bezier(0.65, 0, 0.35, 1) var(--d) both;
	}

	@keyframes draw {
		from {
			stroke-dashoffset: 1;
		}
	}

	@keyframes trace-out {
		0%,
		55% {
			opacity: 1;
		}
		100% {
			opacity: 0;
		}
	}

	@keyframes fill-in {
		from {
			opacity: 0;
		}
	}

	@keyframes scorch {
		0% {
			color: #ffffff;
			filter: drop-shadow(0 0 20px rgba(255, 233, 196, 0.9));
		}
		30% {
			color: var(--laser-core);
			filter: drop-shadow(0 0 16px rgba(255, 122, 24, 0.8));
		}
		60% {
			color: var(--laser);
			filter: drop-shadow(0 0 11px rgba(255, 122, 24, 0.55));
		}
		80% {
			color: #c2410c;
			filter: drop-shadow(0 0 6px rgba(194, 65, 12, 0.35));
		}
		100% {
			color: var(--logo);
			filter: drop-shadow(0 0 0 rgba(0, 0, 0, 0));
		}
	}

	@media (prefers-reduced-motion: reduce) {
		.solid,
		.trace,
		.trace use {
			animation: none;
		}
	}
</style>
