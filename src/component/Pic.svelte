<script>
  import { afterUpdate } from "svelte";
  import { myPic, myName, msg } from "../stores.js";

  //   let picUrl = "";
  let text = "";
  afterUpdate(() => {
     msg.set([
    {
      type: "flex",
      altText: text,
      contents: {
        type: "bubble",
        body: {
          type: "box",
          layout: "vertical",
          contents: [
            {
              type: "image",
              url: $myPic,
              size: "full",
              aspectMode: "cover",
              aspectRatio: "1:1",
              gravity: "center",
            },
            {
              type: "image",
              url:
                "https://scdn.line-apps.com/n/channel_devcenter/img/flexsnapshot/clip/clip15.png",
              position: "absolute",
              aspectMode: "fit",
              aspectRatio: "1:1",
              offsetTop: "0px",
              offsetBottom: "0px",
              offsetStart: "0px",
              offsetEnd: "0px",
              size: "full",
            },
            {
              type: "box",
              layout: "horizontal",
              contents: [
                {
                  type: "box",
                  layout: "vertical",
                  contents: [
                    {
                      type: "box",
                      layout: "horizontal",
                      contents: [
                        {
                          type: "text",
                          text: text,
                          size: "xl",
                          color: "#ffffff",
                          wrap: true,
                        },
                      ],
                    },
                    {
                      type: "box",
                      layout: "vertical",
                      contents: [
                        {
                          type: "box",
                          layout: "vertical",
                          contents: [
                            {
                              type: "text",
                              text: "by " + $myName,
                              color: "#ffffff",
                              size: "md",
                              flex: 0,
                              align: "end",
                              style: "italic",
                            },
                          ],
                          flex: 0,
                          spacing: "lg",
                        },
                      ],
                    },
                  ],
                  spacing: "xs",
                },
              ],
              position: "absolute",
              offsetBottom: "0px",
              offsetStart: "0px",
              offsetEnd: "0px",
              paddingAll: "20px",
            },
          ],
          paddingAll: "0px",
          action: {
            type: "uri",
            label: "action",
            uri: "https://liff.line.me/1654061887-ZoYpPWL2",
          },
        },
      },
    },
  ]);
  })
</script>

<style>
  .box {
    display: flex;
    flex-direction: column;
  }
  .flex-pic-container {
    display: flex;
    height: 300px;
    width: 300px;
    flex-direction: column;
    justify-content: flex-end;
    background: var(--flex-container--bg);
    background-size: contain;
    background-repeat: no-repeat;
  }
  .flex-item {
    display: flex;
    width: auto;
    height: auto;
    flex-wrap: wrap;
  }

  .item2 {
    align-self: flex-end;
  }

  .name {
    font-style: italic;
    font-size: medium;
  }
  .text {
    margin-bottom: 0px;
    font-size: x-large;
  }

  p,
  pre {
    color: aliceblue;
    padding: 0px 20px;
  }

  textarea {
    width: 100%;
  }
</style>

<div class="box">
  <div class="item-input">
    <textarea bind:value={text} placeholder="input..." rows="3" />
  </div>
  <div class="flex-pic-container" style="--flex-container--bg: url({$myPic})">
    <div class="flex-item item1">
      <pre class="text">{text}</pre>
    </div>
    <div class="flex-item item2">
      <p class="name">by {$myName}</p>
    </div>
  </div>
</div>
