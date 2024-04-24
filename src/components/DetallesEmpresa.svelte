<script lang="ts">
  import { slide } from "svelte/transition";

  import { Empresas } from "@data";
  import { createEventDispatcher } from "svelte";

  type Empresa = {
    id: number;
    RFC: string;
    nombre_empresa: string;
    encargado_RH: string;
  };

  export let empresa: Empresa;

  const dispatch = createEventDispatcher();

  function cerrar() {
    dispatch("cerrar");
  }
</script>

<div class="detalles-empresa" transition:slide>
  <button class="btn btn-close" on:click={cerrar}><i class="ri-close-line" /></button>
  <div class="detalles-header">
    <h2>{empresa.nombre_empresa}</h2>
    <p><span>RFC &bull;</span> {empresa.RFC}</p>
    <p>Encargado de RRHH: {empresa.encargado_RH}</p>
  </div>
  <!-- <div class="detalles-contenido">
    <h3>Detalles:</h3>
  </div> -->
</div>

<style>
  .detalles-empresa {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: var(--blanco-200);
    padding: 3rem;
    border-radius: 0.5rem;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    max-height: 600px;
    max-width: 600px;
    z-index: 1000;
  }

  .btn-close {
    position: absolute;
    top: 1rem;
    right: 1rem;
    background-color: transparent;
    border: none;
    cursor: pointer;
  }

  .btn-close i {
    color: var(--rojo-400);
    font-size: 2rem;
  }

  .detalles-header {
    /* border: 1px solid black; */
    /* width: 100%; */
    padding: 1rem;
    height: auto;
    margin-top: 1rem;
  }

  .detalles-header h2 {
    text-align: center;
    font-size: 1.6rem;
    color: var(--dorado-900);
  }

  .detalles-header p {
    font-size: 0.9rem;
    font-weight: 300;
    color: var(--verde-800);
    text-align: end;
  }

  @media (max-width: 768px) {
    .detalles-empresa {
      padding: 1rem;
    }

    .detalles-header h2 {
      font-size: 1.3rem;
    }

    .detalles-header p {
      font-size: 0.8rem;
    }
  }
</style>
