<script lang="ts">
  let isAuthenticated = window.localStorage.getItem('token') !== null;
  let isMenuOpen = false;

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }

  function logoutHandler () {
    console.log('Hello word')
    window.localStorage.removeItem('token');
    window.location.href = '/login';
    isAuthenticated = false;
  }
</script>

<div class="menu-container">
  <div class="menu-toggle">
    <button aria-label="Abrir menu" aria-expanded={isMenuOpen} on:click={toggleMenu}>
      <span class="hamburger">
        <i class="ri-menu-line" class:hidden={isMenuOpen}></i>
        <i class="ri-close-line" class:hidden={!isMenuOpen}></i>
      </span>
    </button>
  </div>

  <nav class="menu" class:open={isMenuOpen}>
    <ul>
      <li><a href="/">Inicio</a></li>
      {#if !isAuthenticated}
        <li><a href="/register">Registrarse</a></li>
        <!-- <li><a href="/login">Iniciar Sesión</a></li> -->
      {/if}
      {#if isAuthenticated}
        <li><a href="/jobFairs">Eventos</a></li>
        <li><a href="/AttedendanceBadge">Gafete</a></li>
        <li><a href="/EventCountdown">Próximo Evento</a></li>
        <li><a href="/ListadoEmpresa">Empresas</a></li>
      {/if}
    </ul>
  </nav>
  {#if isAuthenticated}
    <div class="btn">
      <button class="btn-logout" type="button" on:click={logoutHandler}>Cerrar Sesión</button>
    </div>
  {/if}
  {#if !isAuthenticated}
    <div class="btn">
      <button class="btn-login" type="button" on:click={() => window.location.href = '/login'}>Iniciar Sesión</button>
    </div>
  {/if}
</div>

<style>
  .menu-container {
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .menu ul {
    display: flex;
    list-style: none;
    gap: 1rem;
  }

  .menu ul li a {
    text-decoration: none;
    color: var(--blanco-200);
    transition:
      text-decoration 0.3s ease,
      color 0.3s ease;
  }

  .menu ul li a:hover {
    text-decoration: underline;
    color: var(--dorado-300);
  }

  .menu-toggle {
    display: none;
  }

  .btn .btn-logout {
    background-color: var(--rojo-300);
    color: var(--blanco-50);
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 0.3rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .btn .btn-login {
    background-color: var(--verde-500);
    color: var(--blanco-50);
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 0.3rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .btn .btn-login:hover {
    background-color: var(--verde-300);
  }

  .btn .btn-logout:hover {
    background-color: var(--rojo-500);
  }

  @media (max-width: 768px) {
    .menu-toggle {
      display: block;
    }

    .menu-toggle button {
      background: var(--dorado-300);
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 0.3rem;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .menu-toggle .hamburger i {
      color: var(--blanco-200);
      background: transparent;
    }

    .menu {
      display: none;
      position: absolute;
      top: 9rem;
      left: 0;
      width: 100%;
      background-color: var(--verde-500);
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      transition:
        transform 0.3s ease,
        opacity 0.3s ease;
      transform: scaleY(0);
      transform-origin: top;
      opacity: 0;
    }

    .ri-menu-line.hidden,
    .ri-close-line.hidden {
      display: none;
    }

    .menu.open {
      display: block;
      transform: scaleY(1);
      opacity: 1;
    }

    .menu ul {
      flex-direction: column;
      padding: 1rem 2rem;
      gap: 2rem;
    }
  }
</style>
