<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Max";
  let jobTitle = "Web Developer";
  let description = "I am a web developer";
  let age = 30;
  let userImage;
  let formState = "empty";

  function addContact() {
    if (
      name.trim().length == 0 ||
      jobTitle.trim().length == 0 ||
      description.trim().length == 0 ||
      userImage.trim().length == 0
    ) {
      formState = "invalid";
      return;
    }
    console.log(formState);
    formState = "done";
  }

  // let uppercaseName; not required!

  $: uppercaseName = name.toUpperCase();

  $: console.log(name);

  $: if (name === "Maximilian") {
    console.log("It runs!");
    age = 31;
  }

  function incrementAge() {
    age += 1;
  }

  function changeName() {
    name = "Maximilian";
  }

  function nameInput(event) {
    const enteredValue = event.target.value;
    name = enteredValue;
  }
</script>

<h1>Hello {uppercaseName}, my age is {age}!</h1>
<button on:click={incrementAge}>Change Age</button>
<!-- <button on:click="{changeName}">Change Name</button> -->
<!-- <input type="text" value={name} on:input={nameInput} /> -->
<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={jobTitle} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={userImage} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>

<button on:click={addContact}>Add contact card</button>

{#if formState === "done"}
  <ContactCard userName={name} {jobTitle} {description} {userImage} />
{:else if formState === "invalid"}
  <p>Please fill out all fields</p>
{:else}
  <p>Please enter some data and press the button</p>
{/if}

<style>
  h1 {
    color: purple;
  }

  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>
