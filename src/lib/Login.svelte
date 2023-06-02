<script>
  import { navigate } from "svelte-navigator";

  let userName;
  let password;

  function handleLogin() {
    if (userName === "admin" && password === "admin") {
      navigate("/dashboard");
    }
  }
</script>

<main>
  <input type="text" placeholder="Enter user name" bind:value={userName} />
  <input type="password" placeholder="Enter password" bind:value={password} />
  <button on:click={handleLogin}>Login</button>
</main>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  input {
    margin-bottom: 16px;
  }
</style>
