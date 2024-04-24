<script>
  import DetallesFeria from "@/components/DetallesFeria.svelte";
  import { fade } from 'svelte/transition';

  import { onMount } from 'svelte';

  let ferias  = [];
  let query  = '';
  let filteredFerias = [];
  
  function updateQuery(event) {
    query = event.target.value;
    filteredFerias = ferias.filter(feria => {
      return feria.nombre_evento.toLowerCase().includes(query.toLowerCase());
    });
  }
  
  
  async function getFerias() {
    const response = await fetch('http://127.0.0.1:8000/api/Fair');
    const data = await response.json();
    ferias = data;
    filteredFerias = ferias;
  }
  
  onMount(getFerias);

  let isOpen = false;
  let selectedFeria = null;


  const handleRegister = (feria) => {
    selectedFeria = feria;
    isOpen = true;
  }

</script>

<div class="search">
  <span><i class="ri-search-line"></i></span>
  <input type="search" placeholder="Buscar ferias..." on:input={updateQuery} />
</div>

{#if filteredFerias.length === 0}
  <p>No se encontraron ferias de empleo</p>
{:else}
  <div class="job-fairs">
    {#each filteredFerias as feria}
      <div class="job-fair">
        <h2>{feria.nombre_evento}</h2>
        <p>{feria.descripcion}</p>
        <p><strong>Lugar:</strong> {feria.ubicacion}</p>
        <p><strong>Fecha:</strong> {feria.fecha}</p>
        <button class="register-btn" on:click={() => handleRegister(feria)}>Registrarse</button>
      </div>
    {/each}
  </div>
{/if}


<DetallesFeria bind:isOpen={isOpen} bind:feria={selectedFeria} />

<style>
  .search {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 2.5rem;
  }

  .search span {
    margin-right: 0.4rem;
  }

  .search span i {
    font-size: 1rem;
    color: var(--dorado-900);
  }

  .search input {
    width: 100%;
    padding: 0.5rem;
    border: 1px solid var(--verde-400);
    border-radius: 4px;
  }

  .search input:active {
    transform: scale(1.01);
    transition: transform 0.2s ease;
  }

  .search input:focus {
    outline: none;
    border-color: var(--dorado-700);
    box-shadow: 0 0 2px var(--verde-500);
    transition:
      border-color 0.2s ease,
      box-shadow 0.2s ease;
  }

  .job-fairs {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }

  .job-fair {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: space-between;
    border: 1px solid var(--rojo-200);
    border-radius: 4px;
    padding: 1rem;
    transition:
      box-shadow 0.3s ease,
      transform 0.3s ease;
    overflow: hidden;
  }

  .job-fair h2 {
    text-align: center;
    font-size: 2rem;
    font-weight: bold;
    color: var(--dorado-900);
  }

  /* .job-fair ul {
    list-style-type: square;
    margin-left: 1rem;
  } */

  .job-fair:hover {
    transform: translateY(-5px) scale(1.05);
    box-shadow: 0 8px 16px var(--dorado-700);
  }

  .register-btn {
    margin-top: 0.5rem;
    display: block;
    width: 100%;
    padding: 1rem;
    background-color: var(--verde-500);
    color: var(--blanco-50);
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .register-btn:hover {
    background-color: var(--dorado-700);
  }
</style>
