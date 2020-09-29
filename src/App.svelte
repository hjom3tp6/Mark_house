<script>
  import liff from "@line/liff";
  import { fade } from "svelte/transition";
  import Pic from "./component/Pic.svelte";
  import Social from "./component/Social.svelte";
  import { myPic, myName, msg } from "./stores.js";

  let isInClient = false;
  let liffInit = initLiff();

  const options = [
    { title: "照片", component: Pic },
    { title: "社交", component: Social },
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
  <div class="box-component" transition:fade>
    <h3>Line訊息分享器</h3>
    {#if !isInClient}
      <h1>請移至line中開啟</h1>
    {:else}
      <select bind:value={selected}>
        {#each options as option}
          <option value={option}>{option.title}</option>
        {/each}
      </select>
      <div class ="item-component" transition:fade>
        <svelte:component this={selected.component} />
      </div>
      <button on:click={shareMsg}>share</button>
    {/if}
  </div>
{:catch error}
  <p>{error.message}</p>
{/await}
