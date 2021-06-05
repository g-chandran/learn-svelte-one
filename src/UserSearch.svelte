<script>
  import User from "./User.svelte";

  let userNameQuery = "";
  let user;
  const handleSubmit = (e) => {
    e.preventDefault();

    fetch("https://api.github.com/users/" + userNameQuery)
      .then((result) => result.json())
      .then((data) => (user = data))
      .catch((err) => console.log(err));
  };
</script>

<div class="user-search">
  <h2>Search for users</h2>

  <form on:submit={handleSubmit}>
    <input type="text" bind:value={userNameQuery} />
    <button>Search</button>
  </form>

  {#if user}
    {#if user.login && user.avatar_url}
      <User username={user.login} avatar={user.avatar_url} />
    {:else}
      <p>Invalid Username</p>
    {/if}
  {/if}
</div>

<style>
  .user-search {
    padding: 20px;
    border-radius: 10px;
    margin-bottom: 50px;
    background-color: #efefef;
  }
  h2 {
    margin: 0 0 15px;
  }
</style>
