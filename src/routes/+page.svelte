<script>
  import projects from "$lib/projects.json";
  import Project from "$lib/Project.svelte";

  let profileData = fetch("https://api.github.com/users/g10ria");
</script>

<svelte:head>
  <title>home</title>
</svelte:head>

<h1>Gloria</h1>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolor porro quasi quia consequuntur fugiat ab beatae iusto, mollitia aspernatur, rerum hic consequatur fuga, laudantium incidunt unde quae iste laboriosam recusandae!</p>
<img src="images/spinalcord.jpg" alt="spinal cord"/>

{#await fetch("https://api.github.com/users/g10ria")}
  <p>Loading...</p>
{:then response}
  {#await response.json()}
    <p>Decoding...</p>
  {:then data}
    <section>
      <h2>My GitHub Stats</h2>
      <dl>
        <dt style="text-decoration: underline overline;">Followers:</dt>
        <dd>{data.followers}</dd>
        <dt style="text-decoration: underline overline;">Following:</dt>
        <dd>{data.following}</dd>
        <dt style="text-decoration: underline overline;">Public Repositories:</dt>
        <dd>{data.public_repos}</dd>
      </dl>
    </section>
  {:catch error}
    <p class="error">Something went wrong: {error.message}</p>
  {/await}
{:catch error}
  <p class="error">Something went wrong: {error.message}</p>
{/await}

<h2>projects</h2>
<div class="projects">
{#each projects.slice(0, 3) as p}
<Project data={p} hLevel="3" />
{/each}
</div>