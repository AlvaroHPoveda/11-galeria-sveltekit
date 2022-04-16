<script lang="ts">
  import Card from "../components/Card.svelte";
  import Loading from "../components/Loading.svelte";

  let ref: any;
  let actualPage: number = 1;
  let searchParam: string = "";

  const getImages = async (page: number = 1, searchParam = "park") => {
    if (searchParam.trim() === "") {
      return;
    }
    const res = await fetch(
      `https://api.unsplash.com/search/collections/?query=${searchParam}&page=${page}&per_page=12&client_id=Rp1kC8ixWK07I1Bs-vbP6LLhtiwTBEhE1Qu-z941kkY`
    );
    const data = await res.json();
    return data;
  };

  let promise = getImages();

  const handleSubmit = (e: any) => {
    actualPage = 1;
    promise = getImages(actualPage, searchParam);
  };

  const handleNextPage = () => {
    actualPage++;
    promise = getImages(actualPage, searchParam);
  };

  const handlePrevPage = () => {
    actualPage--;
    promise = getImages(actualPage, searchParam);
  };
</script>

<svelte:head>
  <title
    >Search {searchParam.trim() !== ""
      ? ""
      : `- ${searchParam} Page ${actualPage}`}</title
  >
</svelte:head>

<form on:submit|preventDefault={handleSubmit} class="form-group mb-4 row">
  <div class="col-12 col-md-8">
    <input
      bind:value={searchParam}
      bind:this={ref}
      type="text"
      placeholder="Search Params"
      class="form-control"
      on:focus={() => ref.select()}
    />
  </div>
  <div class="col-12 col-md-4">
    <button type="submit" class="btn btn-dark">Search</button>
  </div>
</form>

<div class="text-center">
  {#await promise}
    <Loading />
  {:then images}
    <div class="row g-3">
      {#each images.results as image}
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
  {:catch}
    <h3>Error</h3>
  {/await}
</div>
