<!--
  # Image

  The `Image` loads images from the from the image folder, and are accessed by name and
  extension using this component. The user's `prefers-color-scheme` setting will be
  respected if set to dark by first attempting to load images from the image/dark directory.

  If no `type` is provided, the type will default to SVG.

  For SVG images in particular, the image will be downloaded and rendered inline, to
  allow customization of the SVG using CSS. The image will also be expanded to fill
  the container. Other images are loaded normally, and will be rendered at their native
  size.

  ## Usage

  ```html
  <div class='icon'
    <Image name-'globe' />
  </div>

  <style>
    .icon {
      width: 2rem;
      height 2rem;
    }
  </style>
  ```
-->

<script module>
  import { writable } from "svelte/store";
  const media = window.matchMedia("(prefers-color-scheme: dark)");
  const darkMode = writable(media.matches);
  media.addListener(({ matches }) => darkMode.set(matches));

  const cachedImages = {};
  function retrieve(src) {
    if (!cachedImages[src]) {
      cachedImages[src] = fetch(src).then((image) => image.text());
    }
    return cachedImages[src];
  }
</script>

<!--
  ## Props

  *   `name`: The name (file name) of the image.
  *   `alt`: The alt text to display in case of failing to load the image.
  *   `type`: The file type (extension) of the image. Default: `svg`
-->

<script>
  const images = Object.fromEntries(
    Object.entries(import.meta.glob("../image/**/*.{png,svg}", { eager: true })).map(
      ([path, value]) => [path.slice("../image/".length), value],
    ),
  );

  let { name, type = "svg", alt } = $props();

  const src = $derived(
    images[`${$darkMode ? "dark/" : ""}${name}.${type}`]?.default ??
      images[`${name}.${type}`]?.default,
  );
  const imageDownload = $derived(retrieve(src));
</script>

{#if type === "svg"}
  <div class="svg">
    {#await imageDownload then image}
      {@html image}
    {/await}
  </div>
{:else}
  <img {src} alt={alt || name} class="image {type}" />
{/if}

<style>
  .image {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    font-size: 0.8rem;
  }

  /* To catch the actual SVG element within the image, as well as an image tag with an SVG src, we include both of these */
  .svg,
  .svg :global(svg) {
    width: 100%;
    height: 100%;
  }
</style>
