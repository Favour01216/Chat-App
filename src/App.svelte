<script>
  import Chatroom from "./Chatroom.svelte";
  import { auth, googleProvider } from "./firebase.js";
  import { authState } from "rxfire/auth";

  let user;

  const unsubscribe = authState(auth).subscribe((usr) => (user = usr));

  function login() {
    auth.signInWithPopup(googleProvider);
  }

  function logout() {
    auth.signOut();
  }
</script>

<main>
  {#if user}
    <Chatroom {user} {logout} />
  {:else}
    <div class="login-form">
      <button on:click={login}
        ><i class="fa fa-google"></i>Login with Google</button
      >
    </div>
  {/if}
</main>

<style>
  main {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
    height: 100%;
    max-width: 400px;
    max-height: 500px;
    background: #fff;
    border: 1px solid #eee;
    box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.1);
  }
  .login-form {
    display: flex; 
   justify-content: center; 
   align-items: center; 
   height: 100%;
  }
  .login-form button {
    padding: 10px 20px;
    background: #4285f4;
    color: #fff;
    border: 1px solid #bbb;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    outline: none;
    text-align: center;
  }
  .login-form button i.fa {
    padding-right: 10px;
    border-right: 1px solid #357ae8;
    color: #555;
  }
</style>
