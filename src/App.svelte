<script>
  import Router from 'svelte-spa-router';
  import Login from './Login.svelte';
  import Home from './Home.svelte';
  import Predict from './Predict.svelte';
  import Upload from './Upload.svelte';

  let routes = {
    '/': Login,
    '/home': Home,
    '/predict': Predict,
    '/upload':Upload
  };
</script>

<main>
  <Router {routes} />
</main>
