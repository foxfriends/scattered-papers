<!--
  # Paper

  The `Paper` component expands to fill its parent container, providing a paper-textured backing
  for its child contents. The paper has a (configurable) shadow.

  ## Usage

  ```html
  <div class='container'>
    <Paper> Content </Paper>
  </div>

  <style>
    .container {
      width: 35rem;
      height: 20rem;
    }
  </style>
  ```
-->

<script>
  const { hmargin = "0", vmargin = "0", children } = $props();
</script>

<!--
  ## Slots

  *   `default`: The contents of the paper.
-->

<div class="paper" style="padding: {vmargin} {hmargin}">
  {@render children()}
</div>

<!--
  ## Styles

  *   `--paper--image`: the image to use as the background for the paper.
  *   `--paper--color`: the color of the paper in the case of no paper image. Default: `#FAFAFA`
  *   `--paper--shadow`: the size of the drop shadow. Default: `0.125rem 0.125rem 0.25rem rgb(0, 0, 0, 0.6)`
-->

<style>
  .paper {
    box-sizing: border-box;
    width: 100%;
    height: 100%;

    position: relative;
    background-color: var(--paper--color, #fafafa);
    background-image: var(--paper--image);
    box-shadow: var(--paper--shadow, 0.125rem 0.125rem 0.25rem rgba(0, 0, 0, 0.6));
  }
</style>
