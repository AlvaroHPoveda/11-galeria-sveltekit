<script lang="ts">
  import Loading from "../components/Loading.svelte";

  import Card from "../components/Card.svelte";

  let actualPage: number = 1;

  const getImages = async (page: number = 1) => {
    const res = await fetch(
      `https://api.unsplash.com/collections/?page=${page}&per_page=12&client_id=Rp1kC8ixWK07I1Bs-vbP6LLhtiwTBEhE1Qu-z941kkY`
    );
    const data = await res.json();
    return data;
  };

  let promise = getImages();

  const handleNextPage = () => {
    actualPage++;
    promise = getImages(actualPage);
  };

  const handlePrevPage = () => {
    actualPage--;
    promise = getImages(actualPage);
  };
</script>

<svelte:head>
  <title>Home - Page {actualPage}</title>
</svelte:head>

<div class="text-center">
  <h1>Galeria SK</h1>
  <hr />
  {#await promise}
    <Loading />
  {:then images}
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
    {#if actualPage !== 1}
      <button on:click={handlePrevPage} class="btn btn-warning">Prev</button>
    {/if}
    <button on:click={handleNextPage} class="btn btn-info">Next</button>
  {/await}
</div>
