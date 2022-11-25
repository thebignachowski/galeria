<script lang="ts">
  import Card from "../components/Card.svelte";

  const getImages = async () => {
    const res = await fetch(
      `https://api.unsplash.com/collections/?page=${1}&per_page=12&
      client_id=W0Df02KNDuGER-8fGqPrg39d-z9wHjio9Ct6AG7d8ko`
    );
    const data = await res.json();
    return data;
  };
</script>

<div class="text-center">
  <h1>Galería SK</h1>
  <!-- svelte-ignore empty-block -->
  {#await getImages() then images}
    <div class="row g-3">
      {#each images as image}
        <div class="col-12 col-md-4">
          <Card
            url={image.cover_photo.urls.thumb}
            title={image.cover_photo.alt_description}
            download={image.cover_photo.urls.full}
          />
        </div>
      {/each}
    </div>
  {/await}
</div>

<style>
  h1 {
    border-bottom: 1px solid #ccc;
  }
</style>
