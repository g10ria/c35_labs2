<script>
import { page } from "$app/stores";
let pages = [
  { url: "./", title: "Home" },
  { url: "./resume", title: "Resume" },
  { url: "./projects", title: "Projects" },
  { url: "./contact", title: "Contact" },
  { url: "https://github.com/g10ria", title: "Github" },
];

let colorScheme = "light dark";
let localStorage = globalThis.localStorage ?? {};
if (localStorage.colorScheme) {
  colorScheme = localStorage.colorScheme;
}
let root = globalThis?.document?.documentElement;
$: root?.style.setProperty("color-scheme", colorScheme);
$: localStorage.colorScheme = colorScheme;
</script>

<nav>
  {#each pages as p}
<a
  href={p.url}
  class:current={"."+$page.route.id === p.url}
  target={p.url.startsWith("http") ? "_blank" : null}
>
  {p.title}
</a>
  {/each}
</nav>
<label class="color-scheme">
		Theme:
		<select bind:value={ colorScheme }>
			<option>light dark</option>
			<option>light</option>
			<option>dark</option>
		</select>
	</label>

<slot />

<style>
nav {
  display: flex;
  margin-bottom: 50px;
  border-bottom-width: 1px;
  border-bottom-style: solid;
  /* border-bottom-color: oklch(80% 3% 200); */
  border-bottom-color: var(--border-color);
}
.current {
  border-bottom-width: 0.4em;
  border-bottom-style: solid;
  border-bottom-color: oklch(80% 3% 200);
  padding-bottom: 0.1em;
}
.color-scheme {
  position: absolute;
  top: 1rem;
  right: 1rem;
  display: inline-flex;
  gap: 4px;
}
</style>