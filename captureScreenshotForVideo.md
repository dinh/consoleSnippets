## capture a screenshot from the video tag
usage: 
1. copy and paste it to console
2. check if video tag is available in console
3. if the video tag is inside an iframe, then inspect the iframe and select the video tag in the elements panel to make it available to console
4. run the function with a string of title

```js
function capture(title) {
        const vid = document.querySelector("video");
        var canvas = document.createElement("canvas");
        canvas.width = vid.videoWidth;
        canvas.height = vid.videoHeight;
        const ctx = canvas.getContext("2d");
        ctx.drawImage(vid, 0, 0, canvas.width, canvas.height);
        const dataURI = canvas.toDataURL("image/jpeg");
        const a = document.createElement("a");
        a.href = dataURI;

        const t = vid.currentTime;
        const ts =
          Math.trunc(t / 60)
            .toString()
            .padStart(2, "0") +
          "_" +
          Math.trunc(t % 60)
            .toString()
            .padStart(2, "0");
        a.download = `screenshot-${title}-${ts}.jpeg`;
        a.click();
}
```
