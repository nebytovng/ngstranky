<script lang="ts">
	import Header from '$lib/components/Header.svelte';
	import HeroSlider from '$lib/components/HeroSlider.svelte';
	import Services from '$lib/components/Services.svelte';
	import NgBot from '$lib/components/NgBot.svelte';
	import Stats from '$lib/components/Stats.svelte';
	import QuickContact from '$lib/components/QuickContact.svelte';
	import Process from '$lib/components/Process.svelte';
	import References from '$lib/components/References.svelte';
	import ClientStats from '$lib/components/ClientStats.svelte';
	import Team from '$lib/components/Team.svelte';
	import Footer from '$lib/components/Footer.svelte';
</script>

<Header />

<!-- Full-width slider — mimo wrapper kvůli overflow:hidden -->
<HeroSlider />

<!-- Mezera pod sliderem -->
<div class="no_title_gap"></div>

<!-- Sekce jsou full-width — každá si sama centruje obsah přes .section-wrap -->

<Services />
<NgBot src="/images/oslava-seda.png" alt="NG dekorátor" bg="seda" />

<Stats />
<NgBot src="/images/posta-bila.png" alt="NG dekorátor" bg="bila" />

<QuickContact />
<NgBot src="/images/ozubeni-seda.png" alt="NG dekorátor" bg="seda" />

<Process />
<NgBot src="/images/kniha-bila.png" alt="NG dekorátor" bg="bila" />

<References />
<NgBot src="/images/megafon.png" alt="NG dekorátor" bg="seda" />

<ClientStats />
<NgBot src="/images/pusa-bila.png" alt="NG dekorátor" bg="bila" />

<Team />

<Footer />
