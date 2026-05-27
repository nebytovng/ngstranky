<script lang="ts">
	import { onMount } from 'svelte';

	const services = [
		{
			id: 'web',
			href: 'https://www.ngstranky.cz/tvorba-webovych-stranek/',
			title: 'Internetové stránky',
			text: 'Klientům vytváříme moderní internetové prezentace založené na profesionálním redakčním systému WordPress s možností velké modulárnosti.',
		},
		{
			id: 'marketing',
			href: 'https://www.ngstranky.cz/internetovy-marketing-seo/',
			title: 'Online marketing, SEO',
			text: 'Skrze nástroje online marketingu se postaráme o to, aby byla Vaše činnost na internetu působivá a efektivní, a získala tak pozornost návštěvníků.',
		},
		{
			id: 'hosting',
			href: 'https://www.ngstranky.cz/webhosting-domenassl-certifikat/',
			title: 'Webhosting, doména, SSL certifikát',
			text: 'Nabízíme rychlý webhosting s denním zálohováním, nadstandardní péčí o klienty, emailové schránky, domény a SSL certifikáty pro bezpečný web.',
		},
	];

	let circleVisible = $state([false, false, false]);
	let sectionEl: HTMLElement | undefined = $state();

	onMount(() => {
		if (!sectionEl) return;

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						/* Staggered reveal: každý kruh se objeví s prodlevou */
						services.forEach((_, i) => {
							setTimeout(() => {
								circleVisible[i] = true;
								circleVisible = [...circleVisible];
							}, i * 200);
						});
						observer.disconnect();
					}
				});
			},
			{ threshold: 0.2 }
		);

		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section class="content_section services-section" id="sluzby" bind:this={sectionEl}>
	<div class="section-wrap">
	<div class="three_columns clearfix">
		{#each services as service, i (service.id)}
			<div class="column1">
				<div class="column_inner">

					<!-- Animovaný kruh s ikonou -->
					<div class="fade_in_circle_holder">
						<a href={service.href} rel="external">
							<div class="fade_in_circle" class:animate_circle={circleVisible[i]}>
								<div class="fade_in_content">
									{#if service.id === 'web'}
										<!-- Globe / www icon -->
										<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 120 120" fill="none" aria-hidden="true">
											<circle cx="60" cy="60" r="44" stroke="white" stroke-width="5"/>
											<ellipse cx="60" cy="60" rx="22" ry="44" stroke="white" stroke-width="5"/>
											<line x1="16" y1="60" x2="104" y2="60" stroke="white" stroke-width="5"/>
											<line x1="16" y1="40" x2="104" y2="40" stroke="white" stroke-width="4"/>
											<line x1="16" y1="80" x2="104" y2="80" stroke="white" stroke-width="4"/>
										</svg>
									{:else if service.id === 'marketing'}
										<!-- Line chart / growth icon -->
										<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 120 120" fill="none" aria-hidden="true">
											<polyline points="12,90 38,60 58,72 80,30 108,20" stroke="white" stroke-width="6" stroke-linejoin="round" stroke-linecap="round" fill="none"/>
											<polyline points="80,20 108,20 108,48" stroke="white" stroke-width="6" stroke-linejoin="round" stroke-linecap="round" fill="none"/>
											<line x1="12" y1="100" x2="108" y2="100" stroke="white" stroke-width="4" stroke-linecap="round"/>
											<line x1="12" y1="100" x2="12" y2="20" stroke="white" stroke-width="4" stroke-linecap="round"/>
										</svg>
									{:else}
										<!-- Monitor / desktop icon -->
										<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 120 120" fill="none" aria-hidden="true">
											<rect x="14" y="18" width="92" height="62" rx="6" stroke="white" stroke-width="5"/>
											<line x1="14" y1="62" x2="106" y2="62" stroke="white" stroke-width="4"/>
											<line x1="44" y1="80" x2="44" y2="98" stroke="white" stroke-width="4" stroke-linecap="round"/>
											<line x1="76" y1="80" x2="76" y2="98" stroke="white" stroke-width="4" stroke-linecap="round"/>
											<line x1="34" y1="98" x2="86" y2="98" stroke="white" stroke-width="4" stroke-linecap="round"/>
										</svg>
									{/if}
								</div>
							</div>
						</a>
					</div>

					<div class="separator transparent" style="margin: 24px 0 25px; height: 1px;"></div>
					<h4 style="text-align: center;">{service.title}</h4>
					<p style="text-align: center;">{service.text}</p>

				</div>
			</div>
		{/each}
	</div>
	</div>
</section>

<style>
	section {
		padding: 80px 0;
		background-color: #fff;
	}

	/* Přepsání šířek sloupců pro tři stejné části */
	.three_columns > .column1 {
		width: 33.33%;
		float: left;
	}

	.column_inner {
		padding: 0 20px;
		text-align: center;
	}

	/* --- Animovaný kruh (z infographer: fade_in_circle) --- */
	.fade_in_circle_holder {
		display: block;
		overflow: hidden;
	}

	.fade_in_circle_holder a {
		display: block;
		overflow: hidden;
	}

	.fade_in_circle {
		display: table;
		width: 212px;
		height: 212px;
		border-radius: 50%;
		background-color: #3c8eba;
		margin: 0 auto;
		opacity: 0;
		transform: scale(0.1);
		transition: opacity 0.4s ease-in-out, transform 0.4s ease-in-out;
		cursor: pointer;
	}

	.fade_in_circle.animate_circle {
		opacity: 1;
		transform: scale(1);
	}

	/* Hover: shake/wobble (původní .animate_shake_hover) */
	.fade_in_circle:hover {
		animation: shake 0.4s ease-in-out;
	}

	@keyframes shake {
		0%   { transform: scale(1) rotate(0deg); }
		25%  { transform: scale(1.05) rotate(-3deg); }
		50%  { transform: scale(1.05) rotate(3deg); }
		75%  { transform: scale(1.05) rotate(-2deg); }
		100% { transform: scale(1) rotate(0deg); }
	}

	/* --- Ikona uvnitř kruhu --- */
	.fade_in_content {
		display: table-cell;
		vertical-align: middle;
		text-align: center;
		width: 100%;
		height: 100%;
		opacity: 0;
		transition: opacity 0.4s ease-in-out 0.2s;
	}

	/* Ikona se zobrazí až po animate_circle */
	.animate_circle .fade_in_content {
		opacity: 1;
	}

	.fade_in_content svg {
		width: 90px;
		height: 90px;
		display: inline-block;
	}

	/* --- Typografie --- */
	h4 {
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		line-height: 20px;
		font-weight: 500;
		color: #262626;
		margin: 0 0 15px;
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
		.three_columns > .column1 {
			width: 100%;
			float: none;
			margin-bottom: 40px;
		}
	}
</style>
