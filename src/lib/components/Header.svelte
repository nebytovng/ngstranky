<script lang="ts">
	let mobileOpen = $state(false);
	let servicesOpen = $state(false);

	const navItems = [
		{ label: 'Domů', href: 'https://www.ngstranky.cz/', active: true },
		{ label: 'Aktuality', href: 'https://www.ngstranky.cz/rubriky/aktuality/' },
		{
			label: 'Nabídka služeb',
			href: null as string | null,
			children: [
				{ label: 'Internetové stránky', href: 'https://www.ngstranky.cz/tvorba-webovych-stranek/' },
				{ label: 'Online marketing, SEO', href: 'https://www.ngstranky.cz/internetovy-marketing-seo/' },
				{ label: 'Webhosting, doména, SSL certifikát', href: 'https://www.ngstranky.cz/webhosting-domenassl-certifikat/' },
				{ label: 'Direct emailing', href: 'https://www.ngstranky.cz/direct-emailing/' },
				{ label: 'Správa sociálních sítí', href: 'https://www.ngstranky.cz/sprava-socialnich-siti/' },
				{ label: 'Monitoring www stránek', href: 'https://www.ngstranky.cz/monitoring-www-stranek/' },
			]
		},
		{ label: 'Vybrané reference', href: 'https://www.ngstranky.cz/reference/' },
		{ label: 'Ohlasy klientů', href: 'https://www.ngstranky.cz/ohlasy/' },
		{ label: 'Kontakt', href: 'https://www.ngstranky.cz/kontakt/' },
	] as const;

	function toggleMobile() {
		mobileOpen = !mobileOpen;
	}
</script>

<header class="page_header">
	<div class="header_outer">
		<div class="section-wrap">
			<div class="header_inner clearfix">

					<!-- Logo -->
					<div class="logo">
						<a href="https://www.ngstranky.cz/" rel="external">
							<img src="/images/ng-logo.png" alt="NG Stránky — Tvorba webových stránek Liberec" />
						</a>
					</div>

					<!-- Desktop navigation -->
					<nav class="main_menu drop_down right" aria-label="Hlavní menu">
						<ul class="clearfix">
							{#each navItems as item (item.label)}
								{#if 'children' in item}
									<li
										class="menu-item has_sub"
										class:open={servicesOpen}
										onmouseenter={() => (servicesOpen = true)}
										onmouseleave={() => (servicesOpen = false)}
									>
										<!-- svelte-ignore a11y_missing_attribute -->
										<a role="button" tabindex="0">{item.label}</a>
										<div
											class="second"
											class:visible={servicesOpen}
											role="menu"
											tabindex="0"
										>
											<div class="inner">
												<div class="inner2">
													<ul>
														{#each item.children as child (child.label)}
															<li class="menu-item" role="menuitem">
																<a href={child.href} rel="external">{child.label}</a>
															</li>
														{/each}
													</ul>
												</div>
											</div>
										</div>
									</li>
								{:else}
									<li class="menu-item" class:active={'active' in item && item.active}>
										<a href={item.href} rel="external" class:current={'active' in item && item.active}>{item.label}</a>
									</li>
								{/if}
							{/each}
						</ul>
					</nav>

					<!-- Mobile hamburger -->
					<button
						class="selectnav_button"
						aria-label="Otevřít menu"
						aria-expanded={mobileOpen}
						onclick={toggleMobile}
					>
						<span></span>
						<span></span>
						<span></span>
					</button>

				</div>
		</div>
	</div>

	<!-- Mobile menu -->
	{#if mobileOpen}
		<nav class="mobile_menu" aria-label="Mobilní menu">
			<ul>
				{#each navItems as item (item.label)}
					{#if 'children' in item}
						<li class="menu-item has-children">
							<span class="mobile-parent">{item.label}</span>
							<ul class="mobile-sub">
								{#each item.children as child (child.label)}
									<li><a href={child.href} rel="external">{child.label}</a></li>
								{/each}
							</ul>
						</li>
					{:else}
						<li class="menu-item">
							<a href={item.href} rel="external" class:current={'active' in item && item.active}>{item.label}</a>
						</li>
					{/if}
				{/each}
			</ul>
		</nav>
	{/if}
</header>

<style>
	/* --- Header shell --- */
	header.page_header {
		width: 100%;
		display: block;
		position: relative;
		z-index: 2000;
		/* box-shadow místo menu_shadow.png z originálu */
		box-shadow: 0 3px 6px rgba(0, 0, 0, 0.35);
		padding: 0 0 3px 0;
	}

	.header_outer {
		background-color: #262626;
		padding: 0 10px;
		display: block;
		z-index: 9000;
	}

	.header_inner {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	/* --- Logo --- */
	.logo {
		height: 80px;
		display: flex;
		align-items: center;
		margin: 0 25px 0 0;
		float: left;
	}

	.logo a {
		display: block;
		height: 75px;
		line-height: 0;
	}

	.logo img {
		height: 100%;
		width: auto;
		display: block;
	}

	/* --- Desktop Nav --- */
	nav.main_menu {
		position: relative;
		z-index: 100;
		float: right;
	}

	nav.main_menu ul {
		list-style: none;
		margin: 0;
		padding: 0;
		display: flex;
	}

	nav.main_menu ul li {
		position: relative;
	}

	nav.main_menu ul li > a {
		font-family: 'Oswald', sans-serif;
		color: #fff;
		font-size: 15px;
		text-decoration: none;
		display: inline-block;
		cursor: pointer;
		line-height: 80px;
		padding: 0 15px;
		margin: 0;
		transition: background-color 0.15s ease, color 0.15s ease;
		white-space: nowrap;
	}

	nav.main_menu ul li:hover > a,
	nav.main_menu ul li.active > a,
	nav.main_menu ul li.open > a {
		color: #fff;
		background-color: #3c8eba;
	}

	nav.main_menu ul li > a.current {
		background-color: #3c8eba;
	}

	/* --- Dropdown submenu --- */
	.has_sub {
		position: relative;
	}

	.second {
		display: none;
		position: absolute;
		top: 80px;
		left: 0;
		z-index: 9999;
		min-width: 220px;
		background-color: #1d1d1d;
	}

	.second.visible {
		display: block;
	}

	.second .inner2 ul {
		display: block;
		list-style: none;
		margin: 0;
		padding: 0;
		min-width: 260px;
	}

	.second .inner2 ul li a {
		font-family: 'Oswald', sans-serif;
		color: #a0a0a0;
		font-size: 13px;
		display: block;
		padding: 10px 20px;
		line-height: 1.4;
		white-space: normal;
		transition: background-color 0.15s ease, color 0.15s ease;
	}

	.second .inner2 ul li a:hover {
		color: #fff;
		background-color: #3c8eba;
	}

	/* --- Mobile hamburger button --- */
	.selectnav_button {
		display: none;
		flex-direction: column;
		justify-content: space-around;
		width: 30px;
		height: 22px;
		background: none;
		border: none;
		cursor: pointer;
		padding: 0;
		float: right;
		margin: 29px 0;
	}

	.selectnav_button span {
		display: block;
		height: 3px;
		background-color: #fff;
		border-radius: 2px;
	}

	/* --- Mobile menu --- */
	nav.mobile_menu {
		background-color: #1d1d1d;
		padding: 10px 0;
	}

	nav.mobile_menu ul {
		list-style: none;
		margin: 0;
		padding: 0;
	}

	nav.mobile_menu ul li a,
	nav.mobile_menu ul li .mobile-parent {
		display: block;
		color: #fff;
		font-family: 'Oswald', sans-serif;
		font-size: 14px;
		padding: 10px 20px;
		border-bottom: 1px solid #333;
		cursor: pointer;
	}

	nav.mobile_menu ul li a:hover {
		background-color: #3c8eba;
	}

	nav.mobile_menu .mobile-sub {
		list-style: none;
		margin: 0;
		padding: 0;
	}

	nav.mobile_menu .mobile-sub li a {
		padding-left: 35px;
		font-size: 13px;
		color: #a0a0a0;
	}

	/* --- Responsive --- */
	@media screen and (max-width: 1024px) {
		nav.main_menu { display: none; }
		.selectnav_button { display: flex; }
	}
</style>
