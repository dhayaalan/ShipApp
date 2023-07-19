<script>
  import axios from 'axios';
  //   import { loginUsername } from '../src/store';
  import { push } from 'svelte-spa-router';

  let username = '';
  let password = '';

  //   function handleLogin() {
  //     console.log('Username:', username);
  //     console.log('Password:', password);
  //   }

  let name = '';
  let pass = '';

  const fetch = async () => {
    const res = await axios({
      method: 'post',
      url: 'http://192.168.0.192:5000/login',
      data: {
        username: username,
        password: password,
      },
    });
    console.log(res.data.password, 'result');
    // loginUsername.set(res.data.loginUsername);
    name = res.data.username;
    pass = res.data.password;

    console.log(name, 'name', pass, 'password');
    Handler(name,pass);
  };

  function Handler(name, pass) {
    if (username == name && password == pass) {
      push('/home');
    } else {
      alert('username and password is incorrect');
    }
  }
</script>

<!-- <Nav /> -->

<div class="container">
  <form class="login-form" on:submit|preventDefault={fetch}>
    <h2>Login Page</h2>
    <div class="form-group">
      <label for="username">Username:</label>
      <input type="text" id="username" bind:value={username} required />
    </div>

    <div class="form-group">
      <label for="password">Password:</label>
      <input type="password" id="password" bind:value={password} required />
    </div>

    <div class="form-group">
      <button type="submit">Login</button>
    </div>
  </form>
</div>

<style>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f2f2f2;
  }

  .login-form {
    background-color: #2b65ece4;
    background-repeat: no-repeat;
    background-size: cover;
    border-radius: 4px;
    padding: 2rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    width: 100%;
    color: black;
    font-family: 'Courier New', Courier, monospace;
  }

  .form-group {
    margin-bottom: 1.5rem;
  }

  .form-group label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
  }

  .form-group input {
    width: 100%;
    padding: 0.75rem;
    font-size: 1rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    transition: border-color 0.3s ease;
  }

  .form-group input:focus {
    outline: none;
    border-color: #0a0a0a;
  }

  .form-group button {
    background-color: #ffffff;
    color: rgb(12, 12, 12);
    border: none;
    border-radius: 4px;
    padding: 0.75rem 1rem;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .form-group button:hover {
    background-color: #fb9dae;
  }

  h2 {
    text-align: center;
  }

  @media (max-width: 600px) {
    .login-form {
      padding: 1rem;
    }

    .form-group label,
    .form-group input,
    .form-group button {
      font-size: 0.9rem;
    }
  }
</style>
