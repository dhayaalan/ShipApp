<script>
  import Nav from './Nav.svelte';
  import axios from 'axios';

  let file = null;

  async function handleUpload() {
    if (file) {
      try {
        const formData = new FormData();
        formData.append('csvfile', file);

        const response = await fetch('http://192.168.0.109:5000/upload', {
          method: 'POST',
          body: formData,
        });

        if (response.ok) {
          const blob = await response.blob();
          const downloadUrl = URL.createObjectURL(blob);
          const link = document.createElement('a');
          link.href = downloadUrl;
          link.download = file.name;
          link.click();
          URL.revokeObjectURL(downloadUrl);
        } else {
          console.error('Error uploading file:', response.status);
        }
      } catch (error) {
        console.error('Error uploading file:', error);
      }

      // Reset the file input
      file = null;
    }
  }

  function handleFileUpload(event) {
    file = event.target.files[0];
  }
</script>

<Nav />

<div class="container">
  <h1>Upload Page</h1>
  <input type="file" class="upload-input" on:change={handleFileUpload} />
  <button on:click={handleUpload}>Upload</button>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }

  .upload-input {
    margin-bottom: 16px;
  }
</style>
