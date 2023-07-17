<script>
  let isLoggedIn = false;

  function handleLogin() {
    isLoggedIn = true;
  }

  function handleLogout() {
    isLoggedIn = false;
  }
</script>

<nav>
  <div>
    <a href="#/home">Home</a>
    <a href="#/predict">Prediction</a>
    <a href="#/upload">Upload</a>
  </div>

  {#if isLoggedIn}
    <button class="logout-button" on:click={handleLogout}>Logout</button>
  {:else}
    <a class="login-link" href="/">Logout</a>
  {/if}
</nav>

<style>
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    background-color: #5072fa;
    color: #fff;
    font-family: 'Times new Roman';
    margin: -8px;
  }

  nav a {
    color: #fff;
    text-decoration: none;
    margin-left: 1rem;
    font-weight: bold;
    transition: opacity 0.3s ease;
  }

  nav a:hover {
    opacity: 0.8;
  }

  .login-link {
    margin-right: 1rem;
  }

  .logout-button {
    background-color: transparent;
    border: none;
    color: #fff;
    cursor: pointer;
    transition: opacity 0.3s ease;
  }

  .logout-button:hover {
    opacity: 0.8;
  }
</style>
