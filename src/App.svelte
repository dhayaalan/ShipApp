<script>
  import Router from 'svelte-spa-router';
  import Login from './Login.svelte';
  import Home from './Home.svelte';
  import Predict from './Predict.svelte';

  let routes = {
    '/': Login,
    '/home': Home,
    '/predict': Predict,
  };
</script>

<main>
  <Router {routes} />
</main>
