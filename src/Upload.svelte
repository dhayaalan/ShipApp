<script>
  import { push } from 'svelte-spa-router';
  import Nav from './Nav.svelte';

  let file;

  async function handleSubmit() {
    if (!file) {
      console.error('No file selected');
      return;
    }

    const formData = new FormData();
    formData.append('file', file);
    console.log(formData);

    try {
      const response = await fetch('http://192.168.0.192:5000/upload', {
        method: 'post',
        body: formData,
      });

      if (response.ok) {
        const data = await response.json();
        console.log(data);
      } else {
        const error = await response.json();
        console.error(error);
      }
    } catch (error) {
      console.error(error);
    }
    push('/home');
  }

  function handleFileChange(event) {
    const fileList = event.target.files;
    if (fileList.length > 0) {
      file = fileList[0];
    } else {
      file = null;
    }
  }
</script>

<Nav />
<main>
  <h1>File Upload</h1>
  <form on:submit|preventDefault={handleSubmit}>
    <input
      type="file"
      accept=".csv, .xlsx, .xls"
      on:change={handleFileChange}
    />
    <button type="submit">Upload</button>
  </form>
</main>

<style>
  main {
    text-align: center;
    padding: 2rem;
  }
</style>
