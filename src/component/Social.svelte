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
      "https://api.thecatapi.com/v1/images/search?format=json&limit=3&size=small",
      {
        headers: catHeaders,
      }
    );
    catPhotots = await res.json();
    console.log(catPhotots[0]);
    p1 = await catPhotots[0].url
    p2 = await catPhotots[1].url
    p3 = await catPhotots[2].url
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
                    url:p3,
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
                        url:p1,
                        size: "full",
                        aspectMode: "cover",
                        aspectRatio: "150:98",
                        gravity: "center",
                      },
                      {
                        type: "image",
                        url:p2,
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
                        url:$myPic,
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
                            text: "brown_05",
                            weight: "bold",
                            color: "#000000",
                          },
                          {
                            type: "span",
                            text: "     ",
                          },
                          {
                            type: "span",
                            text:text,
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
