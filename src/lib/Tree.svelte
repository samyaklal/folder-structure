<script>
  import Branch from "./Branch.svelte";

  export let data;
</script>

<ul>
  {#each data as item}
    <Branch data={item} />
  {/each}
</ul>

<style>
  ul {
    list-style-type: none;
  }
</style>
