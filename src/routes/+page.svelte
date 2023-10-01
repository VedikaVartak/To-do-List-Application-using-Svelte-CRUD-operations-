<script>
  import { Checkbox } from "flowbite-svelte";

  let tasks = [];
  let textInput = "";

  function setEditing(i, isEditing) {
    tasks[i].editing = isEditing;
    tasks[i].text = textInput;
    setEditing(i);
  }

  function saveTask(i) {
    tasks[index].editing = true;
    textInput = tasks[index].text;
  }

  function deleteTask(i) {
    tasks = [...tasks.slice(0, i), ...tasks.slice(i + 1)];
  }

  function create() {
    tasks = [...tasks, { text: textInput, editing: false, checked: false }];
    textInput = "";
  }
</script>

<body>
  <div class="mainWrapper">
    <div class="title">
      <p>To-do List Application</p>
    </div>
    <div style="display:flex; margin: 50px; justify-content: center;">
      <!-- <input type="text" bind:value={textInput} /> -->
      <button type="button" on:click={create}>+ New Task</button>
    </div>
    <div class="listWrapper">
      {#each tasks as task, i}
        <div class="task">
          <div class="checkbox-and-input">
            <div class="checkBox">
              <Checkbox
                unchecked
                class="w-full p-12"
                bind:checked={task.checked}
              />
              <!-- <h4 style="flex-grow: 1">{task.text}</h4> -->
            </div>
            {#if create}
              <input
                type="text"
                class="line-input"
                placeholder="Enter your Task"
                bind:value={task.text}
              />
              <button class="save" on:click={() => saveTask(i)}>Save</button>
            {/if}

            <svg
              class="w-6 h-6 text-gray-800 dark:text-white"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 21 21"
              on:click={() => setEditing(i, false)}
            >
              <path
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M7.418 17.861 1 20l2.139-6.418m4.279 4.279 10.7-10.7a3.027 3.027 0 0 0-2.14-5.165c-.802 0-1.571.319-2.139.886l-10.7 10.7m4.279 4.279-4.279-4.279m2.139 2.14 7.844-7.844m-1.426-2.853 4.279 4.279"
              />
            </svg>

            <svg
              class="w-6 h-6 text-gray-800 dark:text-white"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 18 20"
              on:click={() => deleteTask(i)}
            >
              <path
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M1 5h16M7 8v8m4-8v8M7 1h4a1 1 0 0 1 1 1v3H6V2a1 1 0 0 1 1-1ZM3 5h12v13a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V5Z"
              />
            </svg>
          </div>
        </div>
      {/each}
    </div>
  </div>
</body>

<style>
  body {
    background-color: #e3dffd;
  }

  .title {
    display: flex;
    justify-content: center;
    background-color: #6527be;
    color: aliceblue;
    font-size: 50px;
    height: 120px;
    width: 100%;
    align-items: center;
  }

  .listWrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 10px;
    align-items: center;
    height: 100%;
    margin-top: 50px;
  }

  input {
    background-color: #ecf2ff;
    height: 50px;
    width: 450px;
    border-radius: 15px;
    border: 0;
    padding-left: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .checkBox {
    display: flex;
    align-items: center;
    height: 50px;
  }

  .checkbox-and-input {
    display: flex;
    align-items: center;
    gap: 5px;
  }

  button {
    height: 50px;
    width: 100px;
    top: 80%;
    background-color: #6527be;
    color: aliceblue;
    border: 0;
    border-radius: 7px;
    position: absolute;
    margin: 90px;
    margin-top: 10px;
    margin-left: 600px;
  }
  button:hover,
  .checkBox:hover {
    cursor: pointer;
  }

  svg {
    height: 20px;
    width: 30px;
    color: #6527be;
  }
  svg:hover {
    cursor: pointer;
  }

  /* Add styling for task container */
  .task {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
