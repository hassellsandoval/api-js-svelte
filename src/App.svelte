<script>
  import Cards from "./lib/cards.svelte";
  let caracter=[];
  let pagina=1;
  async function loadcharacters(){
    const response=await fetch("http://rickandmortyapi.com/api/character?page="+pagina)
    const data=await response.json();
    console.log(data)
    caracter=data.results;
  }
  loadcharacters();

  function siguiente(){
  pagina++;
  loadcharacters();
  }

  function anterior(){
    pagina--;
    loadcharacters();
  }
</script>

<h1 class="title">Rick and Morty Svelte</h1>
<h2 class="title">Pagina:{pagina}</h2>

<div class="contenedor">
  <div class="botones">
<button class="boton" on:click={anterior} disabled={pagina===1}>Anterior</button>
<button class="boton" on:click={siguiente}>Siguiente</button>
  </div>
  <div class="grid">
    {#each caracter as caracter }
    <Cards {caracter}/>
       {/each}
  </div>
</div>