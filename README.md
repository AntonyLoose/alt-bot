# alt-bot

A plug-in to automatically add alt captions to images.

## Flow

This will be deleted from the final readme.

1. Get all images
2. Filter images with existing alt tags
3. Process URLS, some may be in format `/some/file/path`, in this case we will need to prepend the website url
3. Send images (urls) for processing
4. Apply returned captions to images

The interface connecting the model should return the following format:

```JSON
{
    [src]: "caption";
    ...
}
```

This format allows us to access the captions efficiently:

```js
const imgs = document.getElementsByTagName("img");
const altless_imgs = Array.from(imgs).filter(img => img.alt); // Any valid alt value ("" is not valid) will result in true
const processed_imgs = altless_imgs.map(img => process_img_src(img));
const captions = process_imgs(altless_imgs);

for (const img of altless_imgs) {
    const caption = captions[img.src];
    img.alt = caption;
}
```
