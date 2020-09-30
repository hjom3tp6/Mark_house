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
    max-width: 85%;
    display: flex;
    margin: auto;
  }

  textarea {
    width: 100%;
  }
  .vertical {
    display: flex;
    flex-direction: row;
  }
  .horizontal {
    display: flex;
    flex-direction: column;
  }
</style>

<div class="box vertical">
  <div class="horizontal">
    <h4>使用 Line flex message simulator製作訊息後貼上json</h4>
    <textarea bind:value={flexMsgJsonString} placeholder="input..." rows="5" />
  </div>
</div>
