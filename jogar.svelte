<svelte:head>
	<link rel="stylesheet" href="/styles/jogar.css">
</svelte:head>

<script>
	import VoltarMenu from './VoltarMenu.svelte'
	import { estado } from "./Estado.js"
	import { trocarEstadoDoJogo } from './Estado.js'


	class EstadoTabela {
		constructor(limiteVerdadeiros, tabela) {
			this.limiteVerdadeiros = limiteVerdadeiros
			this.tabela = tabela
			this.verdadeiros = computarVerdadeiros(tabela)
			this.perdeu = false
		}
	}

	let tabela = [
		["B","?", "?", "B", "?", "B"],
		["?","?", "?", "?", "?", "?"],
		["?","B", "?", "B", "?", "B"],
		["?","?", "?", "B", "?", "?"],
		["B","?", "?", "?", "?", "?"],
		["?","?", "B", "?", "?", "?"],
	]

	let estadoTabela = new EstadoTabela(10, tabela)

	function computarVerdadeiros(tabela) {
		let verdadeiros = 0
		
		for (let i = 0; i < tabela.length; i++) {
			for (let j = 0; j < tabela[i].length; j++) {
				if (tabela[i][j]) {
					verdadeiros++
				}
			}
		}

		return verdadeiros
	}

	function atualizarTabela(i, j) {
		
		if (estadoTabela.tabela[i][j] === '?') {
			estadoTabela.tabela[i][j] = 'L'
		} else if (estadoTabela.tabela[i][j] === 'B') {
			tabela.perdeu = true

			alert("você perdeu !!!")
			trocarEstadoDoJogo("menu")
		}
	}

	function chegouAoFim(estadoTabela) {
		return estadoTabela.verdadeiros === estadoTabela.limiteVerdadeiros
	}

</script>

<h1>
	DESVIE DE 10 BOMBAS PARA GANHAR 
	</h1>

<table>
	{#each estadoTabela.tabela as linha, i}
		<tr>
			{#each linha as dado, j}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<td on:click={() => atualizarTabela(i,j)}>
					{#if dado === '?'}
					<img src="" alt="">
					{:else if dado === 'B' && tabela.perdeu}
					bomba
					{:else if dado === 'L'}
					👍🏼 
					{/if}
				</td>
			{/each}
		</tr>
	{/each}
</table>

<br>

<VoltarMenu/>
