<script lang="ts">
  import ImageDetails from './ImageDetails.svelte';
  let files: any;

  $: pictureInnerHTML = '';

  function handleSelectImageEvent(event) {
    pictureInnerHTML = '<img src="' + event.detail.dataUrl + '" />';
  }
</script>

<div contenteditable='true' bind:innerHTML={pictureInnerHTML} id='img-preview' class='img-preview' />

<ImageDetails on:selectImageEvent={handleSelectImageEvent} />

{#if files && files[0]}
  <p>
    {files[0].name}
  </p>
{/if}

<style>
  .img-preview {
    display: 'block';
  }
</style>
