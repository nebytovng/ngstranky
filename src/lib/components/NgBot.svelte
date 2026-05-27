<script lang="ts">
	interface Props {
		src: string;
		alt?: string;
		bg?: 'seda' | 'bila';
	}

	let { src, alt = 'NG dekorátor', bg = 'bila' }: Props = $props();
</script>

<div class="ngbot-divider" class:seda={bg === 'seda'} class:bila={bg === 'bila'}>
	<img {src} {alt} width="170" height="170" loading="lazy" />
</div>

<style>
	.ngbot-divider {
		text-align: center;
		margin: -1px 0;
		line-height: 0;
	}

	.seda { background-color: #f1f1f1; }
	.bila { background-color: #fff; }

	img {
		display: inline-block;
		width: 170px;
		height: auto;
	}
</style>
