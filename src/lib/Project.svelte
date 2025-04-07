<script>
    export let data = {};
    export let hLevel = 2;
</script>
<article>
    <svelte:element this={"h" + hLevel}>{data.title}</svelte:element>
    <img src={data.image} alt="">
    <p>{data.description}</p>
    <div>{data.year}</div>
</article>

<style>
.projects {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(15em, 1fr));

}
  article {
    margin: 10px;
    grid-template-rows: subgrid;
    grid-row: span 3;
  }
  img {
    max-width: 100%;
  }
</style>