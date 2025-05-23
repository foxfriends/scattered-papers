<!--
  # Text

  The `Text` component renders some text. It is not supported to include tags other than
  text styling tags as the content for this component.

  ## Usage

  ```
  <Text>Hello world</Text>
  ```

  ## Props

  *   `heading`: Flag to use the heading font. Default: `false`
  *   `mono`: Flag to enable the monospaced font. Default: `false`
  *   `accent`: Flag to enable an accent font. Default: `false`
  *   `sc`: Flag to turn on all-small-caps, regardless of font used. Default: `false`
  *   `semibold`: Flag to set weight to semi-bold (500). Default: `false`
-->

<script>
  const {
    heading = false,
    mono = false,
    accent = false,
    sc = false,
    semibold = false,
    children,
  } = $props();
  const classes = $derived(
    Object.entries({ text: true, heading, mono, accent, sc, semibold })
      .filter(([, include]) => include)
      .map(([name]) => name)
      .join(" "),
  );
</script>

<!--
  ## Slots

  *   `default`: The text to render.
-->

{#if heading}
  <h1 class={classes}>
    {@render children()}
  </h1>
{:else}
  <span class={classes}>
    {@render children()}
  </span>
{/if}

<!--
  ## Styles

  *   `--text--font`: The default font to use.
  *   `--text--font-heading`: The heading font to use.
  *   `--text--font-mono`: The monospaced font to use.
  *   `--text--font-accent`: The accent font to use.
-->

<style>
  .text {
    font-family: var(--text--font);
  }

  .heading {
    font-family: var(--text--font-heading);
  }

  .mono {
    font-size: 0.85em;
    font-family: var(--text--font-mono);
    font-variant-numeric: unset;
  }

  .accent {
    font-family: var(--text--font-accent);
  }

  .sc {
    font-variant-caps: all-small-caps;
  }

  .semibold {
    font-weight: 500;
  }
</style>
