<script>
  export let isOpen = false;
  export let feria = null;
</script>


<!-- Modal -->
{#if isOpen}
  <div class="modal" id="modal">
    <div class="modal-content">
      <h3>Confirmar registro en </h3>
      <p>¿Estás seguro de que deseas registrarte en esta feria de empleo?</p>
      <!-- Inicio de la mini encuesta -->
      <div class="survey">
        <form id="survey-form">
          <label for="hear-about">Cómo te enteraste?</label>
          <select id="hear-about" name="hear-about">
            <option value="1">Recomendación</option>
            <option value="2">Busqueda en Internet</option>
            <option value="3">Publicidad en línea</option>
            <option value="4">Redes sociales</option>
            <option value="5">Otros</option>
          </select>
        </form>
      </div>
      <!-- Fin de la mini encuesta -->
      <div class="modal-buttons">
        <button id="confirm-btn">Confirmar</button>
        <button id="cancel-btn" on:click={() => isOpen = false}>Cancelar</button>
      </div>
    </div>
  </div>
{/if}

<style>
  /* Estilos para el modal */
  .modal {
    display: none;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    width: 100%;
    height: 100dvh;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.4);
  }

  .modal-content {
    background-color: #eaeaea;
    padding: 1rem;
    border: 1px solid var(--rojo-100);
    width: 35%;
    position: relative;
    margin: auto;
    transform: translateY(50%);
    top: 10%;
    transition: box-shadow 0.35s ease;
  }

  .modal-content:hover {
    box-shadow: 0 8px 16px var(--rojo-700);
  }
  .modal-content h3 {
    text-align: center;
    font-size: 1.8rem;
    font-weight: bold;
    color: var(--dorado-900);
  }

  .modal-content p {
    font-size: 1.2rem;
    text-align: center;
  }

  .survey {
    height: 4rem;
    width: 100%;
    margin-top: 2rem;
    margin-bottom: 2.5rem;
  }

  #survey-form {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  label {
    font-weight: bold;
    color: var(--verde-500);
  }

  select {
    padding: 0.5rem;
    border: 1px solid var(--verde-400);
    border-radius: 4px;
    cursor: pointer;
  }


  select:active {
    transform: scale(1.05);
    transition: transform 0.2s ease;
  }

  select:focus {
    outline: none;
    border-color: var(--dorado-700);
    box-shadow: 0 0 2px var(--verde-500);
    transition:
      border-color 0.2s ease,
      box-shadow 0.2s ease;
  }

  .modal-buttons {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    margin-top: 1rem;
  }

  .modal-buttons button {
    padding: 0.8rem 1.5rem;
    border-radius: 0.5rem;
    border: none;
    cursor: pointer;
  }

  #confirm-btn {
    background-color: var(--verde-500);
    color: var(--blanco-100);
    transition: background-color 0.3s ease;
  }
  #confirm-btn:hover {
    background-color: var(--verde-400);
    color: var(--blanco-100);
  }

  #cancel-btn {
    background-color: var(--rojo-500);
    color: var(--blanco-100);
  }
  #cancel-btn:hover {
    background-color: var(--rojo-400);
    color: var(--blanco-100);
  }

  @keyframes entrarModal {
    from {
      opacity: 0;
      transform: translateY(-10%);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @keyframes salirModal {
    from {
      opacity: 1;
      transform: translateY(0);
    }
    to {
      opacity: 0;
      transform: translateY(-10%);
    }
  }

  /* Estilos para mobiles */
  @media (max-width: 768px) {
    .modal-content {
      width: 80%;
      padding: 1.1rem;
      top: -25%;
    }

    .modal-buttons {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 1.2rem;
    }

    .modal-buttons button {
      width: 100%;
    }
  }
</style>
