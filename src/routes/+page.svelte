<!-- src/routes/+page.svelte -->
<script lang="ts">
  import { onMount } from "svelte"
  import ThemeIcon from "../lib/ThemeIcon.svelte"
    import { Tooltip, TooltipContent, TooltipShortcut, TooltipTrigger } from "@ui-sdk/svelte";

  let dark = $state(false)

  onMount(() => {
    const s = document.documentElement.dataset.colorScheme
    dark = s === "dark" || (s !== "light" && matchMedia("(prefers-color-scheme: dark)").matches)
  })

  function toggle() {
    dark = !dark
    document.documentElement.dataset.colorScheme = dark ? "dark" : "light"
    localStorage.setItem("color-scheme", dark ? "dark" : "light")
  }

  function onkeydown(e: KeyboardEvent) {
    if (e.key.toLowerCase() !== "h" || e.metaKey || e.ctrlKey || e.altKey) return
    if ((e.target as HTMLElement).closest("input, textarea, select")) return
    toggle()
  }
</script>

<svelte:window {onkeydown} />
<div
	class="grid min-h-dvh grid-cols-1 grid-rows-[auto_1fr] border border-border
	       lg:h-dvh lg:grid-cols-[224fr_380fr_245fr] lg:grid-rows-[24fr_442fr]"
>
	<header class="lg:col-start-2 lg:row-start-1"></header>

	<main class="min-w-0 lg:col-start-2 lg:row-start-2">
	<section class="flex items-center justify-between">
  <h2 class="text-base font-medium">Faiyan</h2>

  <nav class="flex gap-25">
      <ol>
          <li class="underline italic">
              <a href="/primer-trim">Primer Trim</a>
          </li>
      </ol>

      <button
          type="button"
          aria-label="Toggle theme"
          onclick={toggle}
          class="text-muted-foreground outline-none transition-colors hover:text-foreground focus-visible:text-foreground"
      >
          <ThemeIcon class="size-4.5 dark:-scale-x-100" />
      </button>
  </nav>

	</section>


	<section class="w-full h-full flex mx-10">
	    <div class="my-8">
	        <h2 class="pb-10 text-bold text-xl">Sobre mi</h2>
	        <p class="pb-4">Soc un noi amb plans ambiciosos per al meu futur.</p>
	        <p class="pb-4">Estudio informàtica i vull continuar aprenent i millorant, anant molt més enllà d'on soc ara.</p>
	        <p class="pb-4">El meu objectiu és estudiar a la Universitat Politècnica de Catalunya i tenir èxit en aquest camí.</p>
		</div>
	</section>

	</main>

	<aside class="hidden lg:□block lg:col-start-1 lg:row-span-2 lg:row-start-1"></aside>

	<aside class="hidden lg:block lg:col-start-3 lg:row-span-2 lg:row-start-1"></aside>
</div>
