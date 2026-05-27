<script lang="ts">
	const references = [
		{
			id: 'renomia',
			img: '/images/renomia-logo-2.png',
			alt: 'Logo renomia.cz - významná mezinárodní společnost v oboru pojištění a risk managementu',
			title: 'renomia.cz',
			categories: 'Online marketing, Programování, WWW stránky',
			href: 'https://www.ngstranky.cz/portfolio_page/renomia-cz/',
		},
		{
			id: 'axa',
			img: '/images/axa-logo-2.png',
			alt: 'Logo Axa assistance - specialisté na cestovní pojištění',
			title: 'AXA Assistance',
			categories: 'Online marketing, Programování, WWW stránky',
			href: 'https://www.ngstranky.cz/portfolio_page/axa-assistance/',
		},
		{
			id: 'bmto',
			img: '/images/BMTO-TECH-sro-logo.png',
			alt: 'Logo BMTO TECH s.r.o.',
			title: 'bmtotech.cz',
			categories: 'WWW stránky',
			href: 'https://www.ngstranky.cz/portfolio_page/bmtotech-cz/',
		},
		{
			id: 'asc',
			img: '/images/as-casting-logo.png',
			alt: 'Logo AS-CASTING s.r.o.',
			title: 'asc.cz',
			categories: 'WWW stránky',
			href: 'https://www.ngstranky.cz/portfolio_page/asc-cz/',
		},
	];
</script>

<section class="content_section references-section" id="reference">
	<div class="section-wrap">

	<!-- Header: nadpis 75% | tlačítko 25% -->
	<div class="two_columns_75_25 clearfix">
		<div class="column1">
			<div class="column_inner">
				<h2>REFERENCE</h2>
				<p>Vybrané reference našich klientů z různých druhů spolupráce.&nbsp;Děkujeme jim za důvěru a přejeme mnoho úspěchů.</p>
				<div class="separator transparent" style="margin-top: 14px; margin-bottom: 10px;"></div>
			</div>
		</div>
		<div class="column2">
			<div class="column_inner">
				<p class="btn-right">
					<a href="https://www.ngstranky.cz/reference" class="button" rel="external">VÍCE ZDE</a>
				</p>
			</div>
		</div>
	</div>

	<!-- Portfolio mřížka — 4 sloupce -->
	<div class="projects-grid">
		{#each references as ref (ref.id)}
			<article class="portfolio-item">
				<div class="img-wrap">
					<a href={ref.href} rel="external">
						<img src={ref.img} alt={ref.alt} loading="lazy" />
					</a>
				</div>
				<!-- Překryvná vrstva při hoveru -->
				<div class="overlay" aria-hidden="true">
					<a href={ref.href} class="overlay-link" rel="external" tabindex="-1">
						<div class="overlay-text">
							<h4>{ref.title}</h4>
							<p>{ref.categories}</p>
						</div>
					</a>
				</div>
			</article>
		{/each}
	</div>

	</div>
</section>

<style>
	section.references-section {
		background-color: #fff;
		padding: 80px 0;
	}

	/* Layout sloupce */
	.two_columns_75_25 { width: 100%; }
	.two_columns_75_25 > .column1 { width: 75%; float: left; }
	.two_columns_75_25 > .column2 { width: 25%; float: left; }
	.column_inner { padding: 0 20px; }

	h2 {
		font-family: 'Oswald', sans-serif;
		font-size: 40px;
		line-height: 40px;
		font-weight: 500;
		color: #262626;
		margin: 0 0 20px;
	}

	p {
		font-family: 'PT Sans', sans-serif;
		font-size: 13px;
		line-height: 22px;
		color: #4f4f4f;
		margin: 0;
	}

	.btn-right {
		text-align: right;
		padding-top: 10px;
	}

	/* Portfolio mřížka */
	.projects-grid {
		display: flex;
		flex-wrap: wrap;
	}

	.portfolio-item {
		width: 25%;
		position: relative;
		overflow: hidden;
		line-height: 0;
	}

	/* Obrázek */
	.img-wrap { display: block; }

	.img-wrap a { display: block; }

	.img-wrap img {
		width: 100%;
		height: 191px;
		object-fit: contain;
		background-color: #f5f5f5;
		display: block;
		line-height: 0;
	}

	/* Překryvná vrstva */
	.overlay {
		position: absolute;
		inset: 0;
		background-color: rgba(30, 30, 30, 0.55);
		opacity: 0;
		transition: opacity 0.5s ease;
	}

	.portfolio-item:hover .overlay {
		opacity: 1;
	}

	.overlay-link {
		display: block;
		width: 100%;
		height: 100%;
		position: relative;
		overflow: hidden;
		text-decoration: none;
	}

	/* Červený pruh vyjíždí zdola */
	.overlay-text {
		position: absolute;
		bottom: -100px;
		left: 0;
		width: 100%;
		background-color: #e91b23;
		transition: bottom 0.4s linear;
	}

	.portfolio-item:hover .overlay-text {
		bottom: 0;
	}

	.overlay-text h4 {
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		line-height: 20px;
		font-weight: 500;
		color: #fff;
		text-align: center;
		margin: 18px 0 0;
	}

	.overlay-text p {
		font-family: 'Oswald', sans-serif;
		font-size: 14px;
		font-weight: 400;
		text-transform: uppercase;
		color: #fff;
		text-align: center;
		margin: 8px 0 12px;
		line-height: 1.3;
	}

	/* Responsive */
	@media screen and (max-width: 1024px) {
		.two_columns_75_25 > .column1,
		.two_columns_75_25 > .column2 {
			width: 100%;
			float: none;
		}

		.btn-right { text-align: left; }

		.portfolio-item { width: 50%; }
	}

	@media screen and (max-width: 768px) {
		.portfolio-item { width: 100%; }

		.img-wrap img { height: 160px; }
	}
</style>
