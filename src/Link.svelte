<!--
  # Link

  The `Link` component encapsulates the regular `<a>` tag, providing the default styling.

  ## Usage

  ```
  <Link href='https://cameldridge.com'>cameldridge.com</Link>
  ```

  ## Props

  *   `href`: The URL this link points to. Default: `undefined`
  *   `external`: Flag to set `target='_blank'` on the link, to open in a new tab. Default: `false`
  *   `download`: Flag to make this link a download link. Default: `false`
  *   `discreet`: Flag that enables a more discreet styling for the link. Default: `false`

  ## Events

  *   `click`: Emitted when the link content is clicked.
-->
<script>
  const {
    href = undefined,
    external = undefined,
    download = undefined,
    discreet = undefined,
    children,
    onclick = undefined,
  } = $props();

  const target = $derived(external ? "_blank" : undefined);

  function doOnClick(e) {
    e.stopPropagation();
    onclick();
  }
</script>

<!--
  ## Slots

  *   `default`: The content to render as a link.
-->

{#if href}
  <a
    onclick={onclick ? doOnClick : undefined}
    {href}
    {target}
    {download}
    class="link {discreet ? 'discreet' : ''}"
  >
    {@render children()}
  </a>
{:else}
  <div onclick={onclick ? doOnClick : undefined} class="link {discreet ? 'discreet' : ''}">
    {@render children()}
  </div>
{/if}

<!--
  ## Styles

  *   `--link--color`: The colour of the link text.
  *   `--link--color-hover`: The colour of the link text when the mouse hovers over it.
-->

<style>
  .link {
    cursor: pointer;
  }

  .link:link,
  .link:visited,
  .link:active {
    color: var(--link--color);
    text-decoration: none;
  }

  .link:hover,
  .link:focus {
    color: var(--link--color-hover);
    text-decoration: underline;
  }

  .link.discreet {
    color: var(--color-ink);
  }
</style>
