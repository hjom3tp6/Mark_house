<script>
  import liff from "@line/liff";
  import { fade } from "svelte/transition";
  import Pic from "./component/Pic.svelte";
  import Social from "./component/Social.svelte";
  import Flex from "./component/Flex-msg-json.svelte";
  import { myPic, myName, msg } from "./stores.js";

  let isInClient = false;
  let liffInit = initLiff();
  let isLogin = false;
  let needlogin = false;
  const options = [
    { title: "照片", component: Pic },
    { title: "貓", component: Social },
    { title: "flex message", component: Flex}
  ];

  let selected = options[0];

  async function initLiff() {
    await liff
      .init({
        liffId: "1654061887-ZoYpPWL2",
      })
      .then(() => {
        // start to use LIFF's api
        displayLiffData();
      })
      .catch((err) => {
        window.alert("請檢察網路連線問題");
      });

    await liff
      .getProfile()
      .then((profile) => {
        myName.set(profile.displayName);
        myPic.set(profile.pictureUrl);
      })
      .catch((err) => {
        console.log("error", err);
      });
  }

  function shareMsg() {
    if (liff.isApiAvailable("shareTargetPicker")) {
      liff
        .shareTargetPicker($msg)
        .then(function (res) {
          console.log(res);
        })
        .catch(function (error) {
          console.log(error);
        });
    }
  }
  function displayLiffData() {
    isInClient = liff.isInClient();
    isLogin = liff.isLoggedIn();
  }

  function login() {
    liff.login();
  }

  function logout() {
    liff.logout();
    window.location.reload();
  }

  $: if (isInClient || isLogin) {
    needlogin = true;
  }
</script>

<style>
  .box-component {
    width: 100%;
    flex-direction: column;
    margin: auto;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>

{#await liffInit}
  <div />
{:then}
  <div class="box-component">
    <h3>Line訊息分享器</h3>
    <!-- {#if !needlogin}
      <button on:click={login}>Login</button>
    {:else} -->
    <div>
      <select bind:value={selected}>
        {#each options as option}
          <option value={option}>{option.title}</option>
        {/each}
      </select>
      <button on:click={shareMsg}>share</button>
    </div>
    <div class="item-component" transition:fade>
      <svelte:component this={selected.component} />
    </div>
    {#if !isInClient}<button on:click={logout}>Logout</button>{/if}
    <!-- {/if} -->
  </div>
{:catch error}
  <p>{error.message}</p>
{/await}
