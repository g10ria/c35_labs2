<script>
  import projects from "$lib/projects.json";
  import Project from "$lib/Project.svelte";
  import Pie from '$lib/Pie.svelte';
  import * as d3 from 'd3';

      let selectedYearIndex = -1;

    let selectedYear;
$: selectedYear = selectedYearIndex > -1 ? pieData[selectedYearIndex].label : null;

  let query = "";
  $: filteredProjects = projects.filter(project => {
	let values = Object.values(project).join("\n").toLowerCase();
	  return values.includes(query.toLowerCase());
  });

  $: filteredByYear = filteredProjects.filter(project => {
        if (selectedYear) {
            return project.year === selectedYear;
        }

        return true;
    });

let pieData;

    $: {
		// Initialize to an empty object every time this runs
        pieData = {};
        
		// Calculate rolledData and pieData based on filteredProjects here
        let rolledData = d3.rollups(filteredProjects, v => v.length, d => d.year);

		// We don't need 'let' anymore since we already defined pieData
        pieData = rolledData.map(([year, count]) => {
            return { value: count, label: year };
        });
    }
</script>

<svelte:head>
  <title>Projects</title>
</svelte:head>

<h1>{ projects.length } projects</h1>
<input type="search" bind:value={query} style="width: 100%"
       aria-label="Search projects" placeholder="🔍 Search projects…" />
<Pie data={pieData} bind:selectedIndex={selectedYearIndex} />
<div class="projects">
    {#each filteredByYear as p}
        <Project data={p} />
    {/each}
</div>