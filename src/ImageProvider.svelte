<script context='module'>
  import { getContext, setContext } from 'svelte';

  const IMAGES = Symbol('Images');

  export const useImages = () => getContext(IMAGES);
</script>

<script>
  export let images;

  setContext(IMAGES, images);
</script>

<slot />
