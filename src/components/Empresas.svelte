<script lang="ts">
  import { Empresas } from "@data";
  import DetallesEmpresa from "@/components/DetallesEmpresa.svelte";
  import { slide } from "svelte/transition";

  type Empresa = {
    id: number;
    RFC: string;
    nombre_empresa: string;
    encargado_RH: string;
  };

  let busqueda: string = "";
  let filteredEmpresas: Empresa[] = Empresas;
  $: filteredEmpresas = Empresas.filter((empresa: Empresa) =>
    empresa.nombre_empresa.toLowerCase().includes(busqueda.toLowerCase())
  );

  // Seleccionar la empresa
  let selectedEmpresa: Empresa | null = null;
  let mostrarDetalles: boolean = false;

  function handleEmpresaSelection(empresa: Empresa) {
    selectedEmpresa = empresa;
    mostrarDetalles = true;
  }

  function cerrarDetalles() {
    mostrarDetalles = false;
  }
</script>

<div class="container">
  <h1>Empresas</h1>

  <div class="search">
    <span><i class="ri-search-line"></i></span>
    <input type="search" bind:value={busqueda} placeholder="Buscar empresa..." />
  </div>

  <table>
    <thead>
      <tr>
        <th>Nombre</th>
        <th>RFC</th>
        <th>Encargado de RRHH</th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      {#each filteredEmpresas as empresa}
        <tr>
          <td>{empresa.nombre_empresa}</td>
          <td>{empresa.RFC}</td>
          <td>{empresa.encargado_RH}</td>
          <td
            ><button on:click={() => handleEmpresaSelection(empresa)} type="button" class="btn primary-btn"
              >Detalles</button
            ></td
          >
        </tr>
      {/each}
    </tbody>
  </table>
</div>

{#if mostrarDetalles && selectedEmpresa !== null}
  <DetallesEmpresa bind:empresa={selectedEmpresa} on:cerrar={cerrarDetalles} />
{:else if mostrarDetalles && selectedEmpresa === null}
  <p>Loading...</p>
{/if}

<style>
  .container {
    max-width: 1024px;
    margin: 0 auto;
    /* padding: 0.6rem 1rem; */
  }

  h1 {
    text-align: center;
    font-size: 3rem;
    color: var(--dorado-900);
  }

  .search {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 2rem;
  }

  .search span {
    margin-right: 0.3rem;
  }

  .search span i {
    font-size: 1.3rem;
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

  table {
    width: 100%;
    border-spacing: 0;
    border-collapse: collapse;
    border: 1px solid var(--dorado-300);
    margin-bottom: 4rem;
  }

  th,
  td {
    padding: 0.5rem;
    border: 1px solid var(--verde-700);
    color: var(--verde-600);
  }

  th {
    text-align: left;
    font-weight: bold;
    color: var(--dorado-800);
    font-size: 1.1rem;
  }

  td {
    font-size: 0.9rem;
    text-align: left;
  }

  .btn {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 1rem 0.8rem;
    border-radius: 0.5rem;
    border: none;
    cursor: pointer;
  }

  .primary-btn {
    background-color: var(--verde-500);
    color: var(--blanco-100);
    transition: background-color 0.3s ease;
  }
  .primary-btn:hover {
    background-color: var(--dorado-300);
    color: var(--blanco-100);
  }

  @media (max-width: 768px) {
    .container {
      padding: 0rem 0.5rem;
    }
    h1 {
      font-size: 2.5rem;
    }
    th {
      font-size: 0.7rem;
    }

    td {
      font-size: 0.6rem;
    }
  }
</style>
