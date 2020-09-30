<script>
  import { afterUpdate } from "svelte";
  import { myName, msg } from "../stores.js";

  let flexMsgJsonString = "";
  let flexMsgJson;

  $: if (flexMsgJsonString) {
    console.log(flexMsgJsonString);
  }
  afterUpdate(async function addMsg() {
    try {
      flexMsgJson = await JSON.parse(flexMsgJsonString);
    } catch (error) {
      console.log("flexMsgJsonString is not a json string");
    }
    msg.set([
      {
        type: "flex",
        altText: $myName + " send a cool message",
        contents: flexMsgJson,
      },
    ]);
  });
</script>

<style>
  .box {
    display: flex;
    flex-direction: column;
    width: 80%;
    align-self: center;
  }

  textarea {
    width: 100%;
  }
</style>

<div class="box">
  <h3>請使用FLEX MESSAGE SIMULATOR製作訊息後貼上</h3>
  <div class="item-input">
    <textarea bind:value={flexMsgJsonString} placeholder="input..." rows="5" />
  </div>
</div>
