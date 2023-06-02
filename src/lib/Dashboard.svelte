<script>
  import Tree from "./Tree.svelte";

  let data = [];
  let folders = [];
  let locations;
  let name;
  let type;
  let location;
  let selectedLocation;
  let isDisabled;

  $: {
    locations = [
      { label: "Select Location" },
      { label: "Root", path: [] },
      ...folders,
    ];
    location = locations.find(({ label }) => label === selectedLocation);
    isDisabled = !(name && type && location?.path);
  }

  function updateData(list, path, prePath) {
    if (path.length) {
      const [first, ...rest] = path;
      const item = list[first];
      return Object.assign([], list, {
        [first]: {
          ...item,
          children: updateData(item.children, rest, [...prePath, first]),
        },
      });
    }

    let item = { label: name, path: [...prePath, list.length] };
    if (type === "Folder") {
      item = { ...item, children: [] };
      folders = [...folders, item];
    }
    return [...list, item];
  }
  function handleSave() {
    data = updateData(data, location.path, []);
    handleCancel();
  }
  function handleCancel() {
    name = "";
    type = "";
    selectedLocation = "Select Location";
  }
</script>

<main>
  <section>
    <h2>Enter details of file/folder to add</h2>
    <div class="form-container">
      <div class="input-container">
        <div>
          <label for="name">Name</label>
          <input type="text" bind:value={name} id="name" />
          <label for="type">Type</label>
          <select bind:value={type} id="type">
            <option value="">Select Type</option>
            <option value="File">File</option>
            <option value="Folder">Folder</option>
          </select>
          <label for="location">Location</label>
          <select bind:value={selectedLocation} id="location">
            {#each locations as { label }}
              <option value={label}>{label}</option>
            {/each}
          </select>
        </div>
      </div>
      <div>
        <button on:click={handleSave} disabled={isDisabled}>Save</button>
        <button on:click={handleCancel}>Cancel</button>
      </div>
    </div>
  </section>
  <section>
    <h2>Folder Structure</h2>
    <Tree {data} />
  </section>
</main>

<style>
  .form-container {
    display: flex;
  }

  .input-container {
    flex-grow: 1;
    display: flex;
    align-items: center;
  }

  input,
  select {
    margin-right: 32px;
  }
</style>
