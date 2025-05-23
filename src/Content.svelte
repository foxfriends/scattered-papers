<script>
  const { children } = $props();
</script>

<div class="content">
  {@render children()}
</div>

<style>
  .content {
    --space: var(--Content--outer-space, 10rem);
    box-sizing: border-box;
    padding: var(--space) 0;
    font-family: var(--font-body);
  }

  /** paragraphs */

  .content > :global(p + p) {
    text-indent: 1em;
  }

  .content > :global(* + *) {
    margin-top: 1rem;
  }

  .content :global(li > * + *) {
    margin-top: 0.5rem;
  }

  .content > :global(*) {
    margin-left: var(--space);
    margin-right: var(--space);
  }

  .content > :global(div) {
    margin-left: unset;
    margin-right: unset;
  }

  /** inlines */

  .content :global(b),
  .content :global(strong) {
    font-weight: 600;
  }

  .content :global(i),
  .content :global(emph),
  .content :global(cite) {
    font-style: italic;
  }

  .content :global(code),
  .content :global(pre) {
    font-family: var(--font-mono);
    font-variant-numeric: unset;
  }

  .content :global(pre),
  .content :global(:not(pre) > code) {
    font-size: 0.85em;
  }

  .content :global(:not(pre) > code) {
    padding: 0 0.2rem;
  }

  /** Headings */

  .content :global(h1),
  .content :global(h3),
  .content :global(h4) {
    font-family: var(--font-display);
  }

  .content :global(h1) {
    font-size: var(--font-size-title);
    margin-left: 2rem;
  }

  .content :global(h2) {
    font-family: var(--font-sub-display);
    font-size: var(--font-size-subtitle);
    text-transform: lowercase;
    margin-right: 2rem;
    letter-spacing: -0.01em;
    text-align: right;
  }

  .content :global(h3) {
    font-size: var(--font-size-heading);
    margin-top: 4rem;
    font-weight: 500;
  }

  .content :global(h4) {
    font-size: var(--font-size-subheading);
    margin-top: 3rem;
    font-weight: 600;
  }

  .content :global(h5) {
    font-family: var(--font-accent);
    font-size: var(--font-size-subheading);
    margin-top: 2rem;
    margin-bottom: -0.5rem;
  }

  .content :global(h6) {
    font-family: var(--font-accent);
    font-size: var(--font-size-body);
    margin-top: 2rem;
    margin-bottom: -0.5rem;
  }

  /** Figures */

  .content :global(figure) {
    display: flex;
    flex-direction: column;
    margin: 2em 0;
  }

  .content :global(figcaption) {
    display: block;
    align-self: flex-end;
    font-family: var(--font-body);
    font-size: var(--font-size-note);
    text-align: right;
    margin-top: -0.6rem;
    padding: 0 2rem;
    border-bottom: 1px solid rgba(0, 0, 0, 0.2);
  }

  /** Rules */

  .content :global(hr) {
    border: none;
    height: 1px;
    width: 14rem;
    background-color: var(--rule--color);
    opacity: 0.5;
    margin: 2rem auto;
  }

  /** Lists */

  .content :global(li ul),
  .content :global(li ol) {
    margin-left: 0;
    padding-left: 2em;
  }

  .content :global(li) {
    margin-left: 0;
    padding-left: 0;
  }

  .content :global(li + li) {
    margin-top: 0.5rem;
  }

  .content :global(ul > li) {
    list-style-type: disc;
  }

  .content :global(li::before) {
    /* base.css styles lists a bit different, so we have to revert that */
    content: unset;
  }

  .content :global(ol > li) {
    list-style: latin;
  }

  /** Def lists */

  .content :global(dl) {
    margin-left: 0;
    padding-left: 0;
  }

  .content :global(dt) {
    font-weight: 500;
  }

  .content :global(dt::before) {
    content: "Def. ";
    font-family: var(--font-accent);
    text-transform: lowercase;
    font-size: 0.85em;
    font-weight: 400;
  }

  .content :global(dd) {
    display: block;
    margin-left: 2rem;
  }

  /** Code */

  .content :global(pre) {
    position: relative;
    padding: 1em;
    max-width: 80ch;
    margin-left: auto;
    margin-right: auto;
    background-color: var(--color__one-dark--black);
    color: var(--color__one-dark--white);
    overflow-x: auto;
  }

  .content :global(pre code) {
    display: block;
    width: 80ch;
  }

  .content :global(pre code::after) {
    position: absolute;
    content: attr(data-language);
    right: 2em;
    bottom: 0em;
  }

  /** Quotes */

  .content :global(blockquote) {
    margin-left: calc(var(--space) + 1rem);
    padding-left: 1rem;
    padding-top: 1rem;
    padding-bottom: 1rem;
    border-left: 3px groove rgba(0, 0, 0, 0.5);
  }

  .content :global(blockquote p:first-child) {
    margin-top: 0;
  }

  .content :global(blockquote p) {
    margin-left: 0;
    margin-right: 0;
  }

  .content :global(a:link),
  .content :global(a:visited),
  .content :global(a:active) {
    color: var(--link--color);
    text-decoration: underline;
    text-decoration-color: color(from var(--link--color) srgb r g b / 0.3);
  }

  .content :global(a:focus),
  .content :global(a:hover) {
    color: var(--link--color-hover);
    text-decoration: underline;
    text-decoration-color: var(--link--color-hover);
  }

  /** Tables */

  .content :global(table) {
    margin: 2rem 0;
    line-height: 1.3;
  }

  .content :global(table),
  .content :global(thead),
  .content :global(tbody),
  .content :global(tr),
  .content :global(td),
  .content :global(th) {
    border-collapse: collapse;
    border-spacing: 0;
  }

  .content :global(th) {
    font-weight: 600;
  }

  .content :global(td),
  .content :global(th) {
    border-bottom: 1px solid rgba(0, 0, 0, 0.5);
    border-top: 1px solid rgba(0, 0, 0, 0.5);
    padding: 0.6rem 1rem;
    font-variant-numeric: lining-nums tabular-nums;
  }
</style>
