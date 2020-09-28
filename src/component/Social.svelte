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
                type: "box",
                layout: "horizontal",
                contents: [
                  {
                    type: "box",
                    layout: "vertical",
                    contents: [
                      {
                        type: "image",
                        url: $myPic,
                        aspectMode: "cover",
                        size: "full",
                      },
                    ],
                    cornerRadius: "100px",
                    width: "72px",
                    height: "72px",
                  },
                  {
                    type: "box",
                    layout: "vertical",
                    contents: [
                      {
                        type: "text",
                        contents: [
                          {
                            type: "span",
                            text: $myName,
                            weight: "bold",
                            color: "#000000",
                          },
                          {
                            type: "span",
                            text: "     ",
                          },
                          {
                            type: "span",
                            text: text,
                          },
                        ],
                        size: "sm",
                        wrap: true,
                      },
                      {
                        type: "box",
                        layout: "baseline",
                        contents: [
                          {
                            type: "text",
                            text: "1,140,753 Like",
                            size: "sm",
                            color: "#bcbcbc",
                          },
                        ],
                        spacing: "sm",
                        margin: "md",
                      },
                    ],
                  },
                ],
                spacing: "xl",
                paddingAll: "20px",
              },
            ],
            paddingAll: "0px",
          },
        },
      },
    ]);
  });
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

  pre {
    white-space: pre-wrap;
  }

  textarea {
    width: 100%;
  }
</style>

<div class="box">
  <div class="item-input">
    <textarea bind:value={text} placeholder="input..." rows="2" />
  </div>
  <!-- <div class="flex-pic-container" style="--flex-container--bg: url({$myPic})">
    <div class="flex-item item1">
      <pre class="text">{text}</pre>
    </div>
    <div class="flex-item item2">
      <p class="name">by {$myName}</p>
    </div>
  </div> -->
</div>
