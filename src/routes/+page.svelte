<script>
  import projects from "$lib/projects.json";
  import Project from "$lib/Project.svelte";

  let profileData = fetch("https://api.github.com/users/g10ria");

  import { onMount } from "svelte";

  let githubData = null;
  let loading = true;
  let error = null;

  onMount(async () => {
    try {
      const response = await fetch("https://api.github.com/users/g10ria");
      githubData = await response.json();
    } catch (err) {
      error = err;
    }
    loading = false;
  });

</script>

<svelte:head>
  <title>home</title>
</svelte:head>

<h1>Gloria</h1>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolor porro quasi quia consequuntur fugiat ab beatae iusto, mollitia aspernatur, rerum hic consequatur fuga, laudantium incidunt unde quae iste laboriosam recusandae!</p>
<img src="images/spinalcord.jpg" alt="spinal cord"/>

{#if loading}
    <p>Loading...</p>
{:else if error}
    <p class="error">Something went wrong: {error.message}</p>
{:else}
    <section>
        <h2>My GitHub Stats</h2>
        <dl>
            <dt>Followers</dt>
            <dd>{githubData.followers}</dd>
            <dt>Following</dt>
            <dd>{githubData.following}</dd>
            <dt>Public Repositories</dt>
            <dd>{githubData.public_repos}</dd>
        </dl>
    </section>
{/if}

<h2>projects</h2>
<div class="projects">
{#each projects.slice(0, 3) as p}
<Project data={p} hLevel="3" />
{/each}
</div>