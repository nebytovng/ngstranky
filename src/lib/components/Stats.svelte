<script lang="ts">
	import { onMount } from 'svelte';

	interface StatItem {
		id: string;
		/* Cílová hodnota čísla */
		target: number;
		/* Formátovaný label (s tečkami jako oddělovač tisíců) */
		label: string;
		title: string;
		text: string;
		link?: { href: string; label: string };
	}

	const stats: StatItem[] = [
		{
			id: 'visitors',
			target: 500000,
			label: '500.000',
			title: 'NÁVŠTĚVNÍKŮ',
			text: 'Každý měsíc navštíví námi zrealizované internetové stránky a elektronické obchody tisíce návštěvníků.',
		},
		{
			id: 'web-price',
			target: 3000,
			label: '3.000',
			title: 'TVORBA WWW STRÁNEK',
			text: 'Od takové ceny jsme Vám schopni připravit www stránky, které budou atraktivní pro návštěvníka.',
			link: { href: 'https://www.ngstranky.cz/tvorba-webovych-stranek/', label: 'Více zde' },
		},
		{
			id: 'hosting-price',
			target: 1190,
			label: '1.190',
			title: 'PROVOZ WWW STRÁNEK',
			text: 'Za necelou stokorunu měsíčně získáte extrémně rychlý a bezpečný webhosting s denním zálohováním.',
			link: { href: 'https://www.ngstranky.cz/webhosting-domenassl-certifikat/', label: 'Více zde' },
		},
	];

	/* Aktuální zobrazené hodnoty (animované) */
	let displayed = $state<string[]>(stats.map(() => '0'));
	let visible = $state(false);
	let sectionEl: HTMLElement | undefined = $state();

	/** Formátuje číslo česky: 500000 → '500.000' */
	function formatCzech(n: number): string {
		return Math.round(n)
			.toString()
			.replace(/\B(?=(\d{3})+(?!\d))/g, '.');
	}

	function animateCounters() {
		const duration = 2000; // ms
		const start = performance.now();

		function step(now: number) {
			const elapsed = Math.min(now - start, duration);
			const progress = elapsed / duration;
			/* easeOutQuart pro přirozené zpomalení na konci */
			const eased = 1 - Math.pow(1 - progress, 4);

			displayed = stats.map((s) => formatCzech(s.target * eased));

			if (progress < 1) requestAnimationFrame(step);
			else displayed = stats.map((s) => s.label);
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
						animateCounters();
						observer.disconnect();
					}
				});
			},
			{ threshold: 0.3 }
		);

		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section
	class="content_section info-section"
	id="informace"
	bind:this={sectionEl}
>
	<div class="section-wrap">
		<h2>INFORMACE O NÁS</h2>
		<div class="separator transparent" style="margin: 5px 0;"></div>

		<div class="three_columns clearfix">
			{#each stats as stat, i (stat.id)}
				<div class="column1">
					<div class="column_inner">
						<div class="counter_holder center" class:visible>
							<span class="counter">{displayed[i]}</span>
							<h4>{stat.title}</h4>
							<p>
								{stat.text}{#if stat.link}
									<strong><a href={stat.link.href} rel="external"> {stat.link.label}</a></strong>
								{/if}
							</p>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<style>
	section.info-section {
		background-color: #f1f1f1;
		padding: 80px 0;
	}

	/* Přepsání šířek sloupců */
	.three_columns > .column1 {
		width: 33.33%;
		float: left;
	}

	.column_inner {
		padding: 0 20px;
	}

	/* --- Counter holder (z infographer: counter_holder) --- */
	.counter_holder {
		display: block;
		opacity: 0;
		transition: opacity 0.6s ease 0.2s;
		width: 100%;
		text-align: center;
	}

	.counter_holder.visible {
		opacity: 1;
	}

	/* --- Číslo (counter) --- */
	.counter {
		font-family: 'Oswald', sans-serif;
		font-size: 96px;
		line-height: 96px;
		height: 96px;
		color: #3c8eba;
		display: block;
		text-align: center;
		overflow: hidden;
		font-weight: 400;
		/* Pevná šířka znaku aby čísla neposkakovala */
		font-variant-numeric: tabular-nums;
	}

	h2 {
		font-family: 'Oswald', sans-serif;
		font-size: 40px;
		line-height: 40px;
		margin: 0 0 20px;
		color: #262626;
		font-weight: 500;
		text-align: left;
	}

	h4 {
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		line-height: 20px;
		font-weight: 500;
		color: #262626;
		margin: 10px 0 15px;
		text-align: center;
	}

	p {
		font-family: 'PT Sans', sans-serif;
		font-size: 13px;
		line-height: 22px;
		color: #4f4f4f;
		text-align: center;
		margin: 0;
	}

	a {
		color: #3c8eba;
	}

	a:hover {
		color: #e91b23;
	}

	/* --- Responsive --- */
	@media screen and (max-width: 1024px) {
		.three_columns > .column1 {
			width: 100%;
			float: none;
			margin-bottom: 40px;
		}
	}

	@media screen and (max-width: 768px) {
		.counter { font-size: 64px; line-height: 64px; height: 64px; }
	}
</style>
