<script lang="ts">
  import { onMount } from "svelte";

  export let title = "FRANCO";
  export let tagline = "Eat  |  Drink  |  Enjoy";
  export let ctaText = "View Our Menu";
  export let ctaHref = "/dinner-menu";
  export let showScrollIndicator = true;

  let visible = false;

  onMount(() => {
    setTimeout(() => {
      visible = true;
    }, 100);
  });
</script>

<section
  class="h-screen bg-hero-pattern bg-cover bg-center bg-no-repeat bg-fixed flex flex-col justify-center items-center text-center px-4 relative"
>
  <!-- Gradient Overlay -->
  <div
    class="absolute inset-0 bg-gradient-to-b from-transparent via-darker/20 to-darker"
  ></div>

  <!-- Content -->
  <div
    class="z-10 transition-all duration-1000 ease-out"
    class:opacity-0={!visible}
    class:opacity-100={visible}
    class:translate-y-8={!visible}
    class:translate-y-0={visible}
  >
    <h1
      class="font-serif text-6xl md:text-8xl lg:text-9xl text-white mb-6 tracking-tighter drop-shadow-2xl"
    >
      {title}
    </h1>

    <div
      class="h-1 w-20 md:w-32 bg-gold mx-auto mb-8 shadow-[0_0_15px_rgba(197,160,89,0.5)]"
    ></div>

    <p
      class="font-sans text-sm md:text-xl text-gray-200 tracking-[0.4em] uppercase font-light drop-shadow-lg mb-10"
    >
      {tagline}
    </p>

    <a href={ctaHref} class="btn-primary inline-block">
      {ctaText}
    </a>
  </div>

  <!-- Scroll Indicator -->
  {#if showScrollIndicator}
    <button
      type="button"
      aria-label="Scroll to content"
      on:click={() => {
        const content = document.getElementById("content");
        if (content) content.scrollIntoView({ behavior: "smooth" });
      }}
      class="absolute bottom-12 group cursor-pointer animate-bounce z-10 bg-transparent border-none"
    >
      <div
        class="w-8 h-14 border-2 border-gray-400 rounded-full flex justify-center p-2 group-hover:border-gold transition-colors"
      >
        <div
          class="w-1 h-3 bg-white rounded-full group-hover:bg-gold transition-colors"
        ></div>
      </div>
    </button>
  {/if}
</section>
