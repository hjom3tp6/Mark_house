<script>
  import { onMount } from "svelte";
  import { myPic } from "../stores.js";

  //   let picUrl = "";
  let name = "";
  let text = "";
  let picUrl = "";
  onMount(async () => {
    await liff
      .getProfile()
      .then((profile) => {
        name = profile.displayName;
        picUrl = profile.pictureUrl;
      })
      .catch((err) => {
        console.log("error", err);
      });
  });

  async function shareMsg() {
    if (liff.isApiAvailable("shareTargetPicker")) {
     await liff
        .shareTargetPicker([
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
                    url: picUrl,
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
                                    text: "by " + name,
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
        ])
        .then()
        .catch(function (res) {
          isInClient = "err";
        });
    }
  }
</script>

<style>
  .flex-container {
    display: -webkit-flex;
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

  p {
    color: aliceblue;
    padding: 0px 20px;
  }
</style>

<input bind:value={text} placeholder="input..." />
<button on:click={shareMsg}>share</button>
<div class="flex-container" style="--flex-container--bg: url({picUrl})">
  <div class="flex-item item1">
    <p class="text">{text}</p>
  </div>
  <div class="flex-item item2">
    <p class="name">by {name}</p>
  </div>
</div>
