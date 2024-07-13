

<script>
  import Modal from "./Update.svelte";
  let showModal = false;
  let editableUser = { id: null, name: "", email: "" };
  export let names;
  export let form;

  const handleUpdate = (/** @type {{ id: null; name: string; email: string; }} */ data) => {
    showModal = true;
    editableUser = { ...data };
    console.log(editableUser);
  };
</script>

<div
  class="mt-10 pt-10 w-full max-w-xl p-5 mx-auto rounded-lg shadow-xl dark:bg-white/10 bg-white/30 ring-1 ring-gray-900/5 backdrop-blur-lg"
>
  <div class="flex items-center justify-between mb-4">
    <div class="space-y-1">
      <h2 class="text-xl font-semibold">List of Users</h2>
      <p class="text-sm text-gray-500">Fetched {names.length} users</p>
    </div>
  </div>
  <table class="min-w-full divide-y divide-gray-200">
    <thead>
      <tr>
        <th
          class="px-6 py-3 text-left text-xs font-medium text-black uppercase tracking-wider"
          >Name</th
        >
        <th
          class="px-6 py-3 text-left text-xs font-medium text-black uppercase tracking-wider"
          >Email</th
        >
        <th
          class="px-6 py-3 text-left text-xs font-medium text-black uppercase tracking-wider"
          >Actions</th
        >
      </tr>
    </thead>
    <tbody class="bg-white divide-y divide-gray-200">
      {#each names as user (user.id)}
        <tr>
          <td class="px-4 py-4 ">{user.name}</td>
          <td class="px-4 py-4 ">{user.email}</td>
          <td class="px-4 py-4 ">
            <form method="GET" action="/profiles?/update" class="inline-block">
              <button type="submit" on:click={() => handleUpdate(user)}>
                <img class="w-4 inline" src="./icons8-edit.svg" alt="update" />
              </button>
            </form>
			<form method="POST" action="/profiles?/delete" class="inline-block ml-3">
				<input type="hidden" name="id" value={user.id} />
				<button type="submit">
				  <img class="w-4 inline" src="./trash-can.svg" alt="delete" />
				</button>
			  </form>
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>

<Modal bind:showModal>
  <h2 slot="header" class="font-bold">UPDATE DATA</h2>
  <form method="post" action="/profiles?/update">
    <div class="flex flex-wrap -mx-3 mb-2">
		<div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
        <label
          class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
          for="grid-city"
        >
          Name
        </label>
        <input
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
          id="name"
          type="text"
          placeholder="Enter name"
          name="name"
          bind:value={editableUser.name}
        />
      </div>
      <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
        <label
          class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
          for="grid-city"
        >
          Email
        </label>
        <input
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
          id="email"
          type="text"
          placeholder="Enter email"
          name="email"
          bind:value={editableUser.email}
        />
      </div>
      <input type="hidden" name="id" value={editableUser.id} />
      <button
        type="submit"
        class="bg-yellow-500 hover:bg-green-700 text-white font-bold mt-5 ml-2 px-2 rounded"
      >
        Save Changes
      </button>
    </div>
  </form>
  {#if form?.success}
    <!-- this message is ephemeral; it exists because the page was rendered in
	   response to a form submission. it will vanish if the user reloads -->
    <p class="pt-2 text-green-600 font-normal">Information Updated!</p>
  {/if}
</Modal>
