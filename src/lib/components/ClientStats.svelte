<script lang="ts">
	import { onMount } from 'svelte';

	const charts = [
		{
			id: 'stranky',
			percent: 95,
			title: 'VYTVOŘENÍ STRÁNEK, ESHOPU',
			text: 'V dnešní době je již téměř nemyslitelné neprezentovat se v online světě formou www stránek nebo elektronického obchodu.',
		},
		{
			id: 'seo',
			percent: 65,
			title: 'OPTIMALIZACE PRO VYHLEDÁVÁNÍ',
			text: 'Většina klientů se chce zviditelnit ve výsledcích vyhledávání, ale zbytečně vynakládá finance do cest, které nemají efekt.',
		},
		{
			id: 'ppc',
			percent: 48,
			title: 'PPC REKLAMA',
			text: 'PPC reklama (platba za proklik) v různé formě je velmi efektivní, a pokud je svěřena odborníkům, přinese Vám velký nárůst návštěvnosti.',
		},
		{
			id: 'konverze',
			percent: 15,
			title: 'KONVERZE, NÁVRATNOST INVESTIC',
			text: 'Skrze efektivní kampaně Vám pomůžeme oslovit ty správné lidi a přeměnit Vaše návštěvníky v zákazníky, kteří se k vám budou rádi vracet.',
		},
	];

	const R = 70;
	const CX = 85;
	const CY = 85;
	const CIRC = 2 * Math.PI * R; // ≈ 439.82

	let animated = $state<number[]>(charts.map(() => 0));
	let visible = $state(false);
	let sectionEl: HTMLElement | undefined = $state();

	function animateCharts() {
		const duration = 1500;
		const start = performance.now();

		function step(now: number) {
			const elapsed = Math.min(now - start, duration);
			const t = elapsed / duration;
			const eased = 1 - Math.pow(1 - t, 3); // easeOutCubic

			animated = charts.map((c) => c.percent * eased);

			if (t < 1) requestAnimationFrame(step);
			else animated = charts.map((c) => c.percent);
		}

		requestAnimationFrame(step);
	}

	onMount(() => {
		if (!sectionEl) return;

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting && !visible) {
						visible = true;
						animateCharts();
						observer.disconnect();
					}
				});
			},
			{ threshold: 0.2 }
		);

		observer.observe(sectionEl);
		return () => observer.disconnect();
	});

	function dashoffset(pct: number): number {
		return CIRC * (1 - pct / 100);
	}
</script>

<section class="content_section client-stats-section" id="statistika" bind:this={sectionEl}>
	<div class="section-wrap">
		<h2>S ČÍM NÁS KLIENTI OSLOVUJÍ</h2>
		<p>Na základě mnohaletých zkušeností jsme sestavili statistiku toho, jak klienti vnímají potřebu jednotlivých služeb, resp. s jakými požadavky nás oslovují.</p>
		<div class="separator transparent" style="margin: 14px 0 10px;"></div>

		<div class="four_columns clearfix">
			{#each charts as chart, i (chart.id)}
				<div class="column{i + 1}">
					<div class="column_inner">
						<div class="pie_chart_holder" class:visible>

							<!-- SVG kroužkový graf (náhrada za jQuery easy-pie-chart) -->
							<div class="percentage">
								<svg viewBox="0 0 170 170" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
									<!-- šedá stopa -->
									<circle
										cx={CX}
										cy={CY}
										r={R}
										fill="none"
										stroke="#d8d8d8"
										stroke-width="12"
									/>
									<!-- modrý oblouk -->
									<circle
										cx={CX}
										cy={CY}
										r={R}
										fill="none"
										stroke="#e91b23"
										stroke-width="12"
										stroke-linecap="round"
										stroke-dasharray={CIRC}
										stroke-dashoffset={dashoffset(animated[i])}
										transform="rotate(-90 85 85)"
									/>
								</svg>
								<span class="percent-label">{Math.round(animated[i])}%</span>
							</div>

							<div class="pie_chart_text">
								<h4>{chart.title}</h4>
								<p>{chart.text}</p>
							</div>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<style>
	section.client-stats-section {
		background-color: #f1f1f1;
		padding: 80px 0;
	}

	/* Sloupce — orig: .four_columns>.columnN width 25% float left */
	.four_columns > .column1,
	.four_columns > .column2,
	.four_columns > .column3,
	.four_columns > .column4 {
		width: 25%;
		float: left;
	}

	/* Asymetrické odsazení — přesně podle originálu */
	.four_columns > .column1 > .column_inner { padding: 0 16px 0 0; }
	.four_columns > .column2 > .column_inner { padding: 0 10px 0 6px; }
	.four_columns > .column3 > .column_inner { padding: 0 6px 0 10px; }
	.four_columns > .column4 > .column_inner { padding: 0 0 0 16px; }

	/* --- Pie chart holder --- */
	.pie_chart_holder {
		display: block;
		margin: 0;
		opacity: 0;
		transition: opacity 0.3s ease;
		text-align: center;
	}

	.pie_chart_holder.visible {
		opacity: 1;
	}

	/* --- Percentage kruh (171×171, původní rozměry) --- */
	.percentage {
		width: 171px;
		height: 171px;
		margin: 0 auto;
		position: relative;
	}

	.percentage svg {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}

	.percent-label {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		font-family: 'Oswald', sans-serif;
		font-size: 25px;
		color: #333;
		line-height: 1;
		pointer-events: none;
	}

	/* --- Popis pod grafem --- */
	.pie_chart_text {
		text-align: center;
		margin: 39px 0 0;
	}

	h2 {
		font-family: 'Oswald', sans-serif;
		font-size: 40px;
		line-height: 40px;
		font-weight: 500;
		color: #262626;
		margin: 0 0 20px;
	}

	h4 {
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		line-height: 20px;
		font-weight: 500;
		color: #262626;
		margin: 0 0 10px;
	}

	p {
		font-family: 'PT Sans', sans-serif;
		font-size: 13px;
		line-height: 22px;
		color: #4f4f4f;
		margin: 10px 0;
	}

	/* --- Responsive --- */
	@media screen and (max-width: 1024px) {
		.four_columns > .column1,
		.four_columns > .column2,
		.four_columns > .column3,
		.four_columns > .column4 {
			width: 50%;
		}
		.four_columns > .column1 > .column_inner,
		.four_columns > .column2 > .column_inner,
		.four_columns > .column3 > .column_inner,
		.four_columns > .column4 > .column_inner {
			padding: 0 10px;
		}
	}

	@media screen and (max-width: 768px) {
		.four_columns > .column1,
		.four_columns > .column2,
		.four_columns > .column3,
		.four_columns > .column4 {
			width: 100%;
			float: none;
			margin-bottom: 40px;
		}
		.four_columns > .column1 > .column_inner,
		.four_columns > .column2 > .column_inner,
		.four_columns > .column3 > .column_inner,
		.four_columns > .column4 > .column_inner {
			padding: 0;
		}

		h2 { font-size: 28px; line-height: 32px; }
	}
</style>
