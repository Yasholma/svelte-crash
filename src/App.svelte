<script lang="ts">
  import type { IUser } from "./interfaces";

  let firstName = "Code";
  let lastName = "XY";
  let color = "red";

  let isSystemOn = true;

  let users: IUser[] = [
    {
      id: 1,
      name: "Leanne Graham",
      username: "Bret",
      email: "Sincere@april.biz",
    },
    {
      id: 2,
      name: "Ervin Howell",
      username: "Antonette",
      email: "Shanna@melissa.tv",
    },
    {
      id: 3,
      name: "Clementine Bauch",
      username: "Samantha",
      email: "Nathan@yesenia.net",
    },
  ];

  $: name = `${firstName}${lastName}`;
  const toggle = () => {
    color = color === "blue" ? "red" : "blue";
    isSystemOn = !isSystemOn;

    users =
      users.length > 3
        ? users.slice(0, -1)
        : [
            ...users,
            {
              id: 4,
              name: "Patricia Lebsack",
              username: "Karianne",
              email: "Julianne.OConner@kory.org",
            },
          ];
  };
</script>

<main>
  <h1 style="color: {color}">Hello {name}!</h1>

  {#if isSystemOn}
    <p>System Is On</p>
  {:else}
    System is Off
    <p />
  {/if}

  <button on:click={toggle}>change</button>

  <h2>System Users</h2>

  <ul style="list-style-type: none; text-align: left">
    {#each users as user (user.id)}
      <li>{user.id} {user.name}</li>
    {/each}
  </ul>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
