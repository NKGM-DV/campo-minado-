<svelte:head>
	<link rel="stylesheet" href="/styles/menu.css">
</svelte:head>

<script>
	import { estado } from './Estado.js'
	import { trocarEstadoDoJogo } from './Estado.js'
</script>

<h1>
	CAMPO MINADO
</h1>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class='menu' on:click={() => trocarEstadoDoJogo('jogar')}>
	Jogar
</div>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class='menu' on:click={() => trocarEstadoDoJogo('sobre')}>
	Sobre
</div>
<!-- svelte-ignore a11y-click-events-have-key-events -->
