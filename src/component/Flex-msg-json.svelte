<script>
  import { afterUpdate } from "svelte";
  import { myName, msg } from "../stores.js";

  let flexMsgJsonString = "";
  let flexMsgJson;

  $: if (flexMsgJsonString) {
    flexMsgJson = JSON.parse(flexMsgJsonString);
  }
  afterUpdate(() => {
    msg.set([
      {
        type: "flex",
        altText: myName + "send a cool message",
        contents: flexMsgJson,
      },
    ]);
  });
</script>

<style>
  .box {
    display: flex;
    flex-direction: column;
  }

  textarea {
    width: 100%;
  }
</style>

<div class="box">
  <h3>請使用FLEX MESSAGE SIMULATOR製作訊息後貼上</h3>
  <div class="item-input">
    <textarea bind:value={flexMsgJsonString} placeholder="input..." rows="2" />
  </div>
</div>
