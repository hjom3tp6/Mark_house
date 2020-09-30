<script>
  import { onMount, afterUpdate } from "svelte";
  import { myPic, myName, msg } from "../stores.js";

  //   let picUrl = "";
  let text = "";
  let catPhotots = [];
  let catHeaders = new Headers({
    "Content-Type": "application/json",
    "x-api-key": "1eab5a71-8d5d-41a4-b429-6da578c8e331",
  });
  let p1 = "";
  let p2 = "";
  let p3 = "";
  onMount(async () => {
    const res = await fetch(
      "https://api.thecatapi.com/v1/images/search?format=json&limit=3&size=small&mime_types=jpg",
      {
        headers: catHeaders,
      }
    );
    catPhotots = await res.json();
    console.log(catPhotots[0]);
    p1 = await catPhotots[0].url;
    p2 = await catPhotots[1].url;
    p3 = await catPhotots[2].url;
  });

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
                    type: "image",
                    url: p1,
                    size: "5xl",
                    aspectMode: "cover",
                    aspectRatio: "150:196",
                    gravity: "center",
                    flex: 1,
                  },
                  {
                    type: "box",
                    layout: "vertical",
                    contents: [
                      {
                        type: "image",
                        url: p2,
                        size: "full",
                        aspectMode: "cover",
                        aspectRatio: "150:98",
                        gravity: "center",
                      },
                      {
                        type: "image",
                        url: p3,
                        size: "full",
                        aspectMode: "cover",
                        aspectRatio: "150:98",
                        gravity: "center",
                      },
                    ],
                    flex: 1,
                  },
                ],
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
            action: {
              type: "uri",
              label: "action",
              uri: "https://liff.line.me/1654061887-ZoYpPWL2",
            },
          },
        },
      },
    ]);
  });
</script>

<style>
  textarea {
    width: 100%;
  }

  .flex-pic-container {
    width: 300px;
    height: 320px;
    border-radius: 10px;
    background-color: bisque;
  }
  .p1 {
    background: var(--item--p1--bg);
    background-repeat: no-repeat;
    background-size: cover;
    width: 150px;
    height: 200px;
  }
  .p2 {
    background: var(--item--p2--bg);
    background-repeat: no-repeat;
    background-size: cover;
    width: 150px;
    height: 100px;
  }
  .p3 {
    background: var(--item--p3--bg);
    background-repeat: no-repeat;
    background-size: cover;
    width: 150px;
    height: 100px;
  }
  .pic {
    background: var(--item--pic--bg);
    background-repeat: no-repeat;
    background-size: cover;
    width: 80px;
    height: 80px;
    border-radius: 40px;
    margin: 20px;
  }
  .vertical {
    display: flex;
    flex-direction: row;
  }
  .horizontal {
    display: flex;
    flex-direction: column;
  }
  .flex-item-pic {
    height: 200px;
  }
  .flex-box-text {
    margin: 20px;
    max-width: 180px;
  }
  .text1 {
    flex-wrap: wrap;
    max-width: 160px;
  }
  .text2 {
    align-self: flex-end;
    color: lightgray;
  }
</style>

<div class="horizontal">
  <div class="item-input">
    <textarea bind:value={text} placeholder="input..." rows="2" />
  </div>
  <div class="flex-pic-container horizontal">
    <div class="vertical">
      <div class="flex-item-pic vertical">
        <div class="p1" style="--item--p1--bg: url({p1})" />
      </div>
      <div class="flex-item-pic horizontal">
        <div class="p2" style="--item--p2--bg: url({p2})" />
        <div class="p3" style="--item--p3--bg: url({p3})" />
      </div>
    </div>
    <div class="vertical">
      <div class="pic" style="--item--pic--bg: url({$myPic})" />
      <div class="flex-box-text horizontal">
        <div class="text1">{$myName + '   '}{text}</div>
        <div class="text2">1,140,753 Like</div>
      </div>
    </div>
  </div>
</div>
