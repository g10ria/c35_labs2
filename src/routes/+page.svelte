<script>
  import projects from "$lib/projects.json";
  import Project from "$lib/Project.svelte";
</script>

<svelte:head>
  <title>home</title>
</svelte:head>

<h1>Gloria</h1>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolor porro quasi quia consequuntur fugiat ab beatae iusto, mollitia aspernatur, rerum hic consequatur fuga, laudantium incidunt unde quae iste laboriosam recusandae!</p>
<img src="images/spinalcord.jpg" alt="spinal cord"/>

<h2>projects</h2>
<div class="projects">
{#each projects.slice(0, 3) as p}
<Project data={p} hLevel="3" />
{/each}
</div>