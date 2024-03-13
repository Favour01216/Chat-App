<script>
  // Import Firebase from the correct path
  import { db } from "./firebase";

  // Import the necessary operators from rxjs
  import { collectionData } from "rxfire/firestore";
  import { startWith } from "rxjs/operators";

  export let user;
  export let logout;

  // Declare message as a writable store to make it reactive
  import { writable } from "svelte/store";
  let messageStore = writable("");
  let message;

  // Subscribe to changes in the message store
  let unsubscribe;
  $: {
    unsubscribe = messageStore.subscribe((value) => {
      message = value;
    });
  }

  // Initialize chats collection
  const query = db.collection("chats").orderBy("sentAt");
  const chats = collectionData(query, "id").pipe(startWith([]));

  function sendMessage() {
    db.collection("chats").add({
      uid: user.uid,
      message: message,
      avatar: user.photoURL,
      sentAt: +new Date(),
    });
    messageStore.set(""); // Clear the message input
  }
</script>

<main>
  <div class="header">
    <div class="logo">Chatroom</div>
    <button on:click={logout}>Logout</button>
  </div>
  <div class="messages">
    {#each $chats as chat}
      <div class="message {chat.uid === user.uid ? 'my-message' : ''}">
        {#if chat.uid !== user.uid}
          <div class="avatar">
            <img src={chat.avatar} alt="" />
          </div>
        {/if}
        <div class="text">{chat.message}</div>
      </div>
    {/each}
  </div>
  <div class="form">
    <input type="text" bind:value={$messageStore} />
    <button on:click={sendMessage}><i class="fas fa-paper-plane"></i></button>
  </div>
</main>

<style>
  :root {
    --primary-color: #007bff;
    --background-color: #f5f5f5;
    --border-color: #ddd;
    --text-color: #111;
  }

  main {
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  .header,
  .form {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    background-color: var(--background-color);
    border-bottom: 1px solid var(--border-color);
  }

  .header .logo {
    font-size: 1.5rem;
    font-weight: 600;
    color: var(--text-color);
  }
  

  .header button,
  .form button {
    padding: 5px 10px;
    border: 1px solid var(--primary-color);
    background-color: var(--primary-color);
    color: #fff;
    border-radius: 5px;
    cursor: pointer;
    font-size: 15px;
  }

  .form input {
    flex: 1;
    padding: 10px;
    border: none;
    outline: none;
    color: var(--text-color);
  }

  .messages {
    flex: 1;
    overflow-y: auto;
    padding: 10px;
    display: flex;
    flex-direction: column;
  }

  .message {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }

  .message .avatar {
    margin-right: 10px;
  }

  .message .text {
    padding: 10px;
    border-radius: 5px;
    background-color: var(--background-color);
    color: var(--text-color);
    font-size: 13px;
    font-weight: 600;
    max-width: fit-content;
  }

  /* Scrollbar styles */
  .message::-webkit-scrollbar {
    width: 5px;
    background: var(--primary-color);
  }

  .message::-webkit-scrollbar-thumb {
    background: var(--primary-color);
    width: 5px;
  }

  /* Position sent messages to the right */
  .message.my-message {
    justify-content: flex-end;
  }

  /* Position received messages to the left */
  .message:not(.my-message) {
    justify-content: flex-start;
  }

  /* Adjust avatar size */
  .message .avatar img {
    max-width: 24px; 
    max-height: 24px; 
    border-radius: 50%; 
  }

  .message.my-message .text {
    background-color: var(--primary-color);
    color: #fff;
  }
</style> 