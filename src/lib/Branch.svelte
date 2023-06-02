<script>
  import Tree from "./Tree.svelte";

  export let data;
  let label;
  let children;
  $: ({ label, children } = data);
  let show = true;

  function handleToggle() {
    show = !show;
  }
</script>

<li>
  <div on:click={handleToggle}>
    <span class="symbol">
      {#if children}
        {#if show}
          v
        {:else}
          >
        {/if}
      {:else}
        o
      {/if}
    </span>
    <span>{label}</span>
  </div>
  {#if show && children && children.length}
    <Tree data={children} />
  {/if}
</li>

<style>
  .symbol {
    font-weight: bolder;
  }
  li {
    cursor: default;
  }
</style>
