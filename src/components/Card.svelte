<script lang="ts">
    export let url:string, title:string, download:string
</script>

<div class="card" style="width: 18rem;">
  <img src={url} class="card-img-top" alt={title} />
  <div class="card-body">   
    <a href={download} target="_blank" class="btn btn-success">Visualizar Imagen</a>
  </div>
</div>
