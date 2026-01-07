<script lang="ts">
  import { onMount } from "svelte";

  let visible = false;

  const images = [
    {
      src: "https://cloudassetskita.com/uploads/menu-1be2bbe0.jpg",
      alt: "Exquisite Plating",
      label: "Craft",
    },
    {
      src: "https://cloudassetskita.com/uploads/franco-night-316x120-2bf9c6d8.jpg",
      alt: "Restaurant Interior",
      label: "Atmosphere",
    },
    {
      src: "https://cloudassetskita.com/uploads/reservation-44050ffa.jpg",
      alt: "Fine Wines",
      label: "Wine",
    },
  ];

  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            visible = true;
          }
        });
      },
      { threshold: 0.15 }
    );

    const section = document.getElementById("experience");
    if (section) observer.observe(section);

    return () => observer.disconnect();
  });
</script>

<section
  id="experience"
  class="py-24 px-6 bg-darker text-center relative overflow-hidden"
>
  <!-- Decorative Glow -->
  <div
    class="absolute top-0 left-0 w-64 h-64 bg-gold/5 rounded-full blur-3xl -translate-x-1/2 -translate-y-1/2"
  ></div>

  <div class="max-w-6xl mx-auto relative z-10">
    <div
      class="transition-all duration-1000 ease-out"
      class:opacity-0={!visible}
      class:translate-y-8={!visible}
      class:opacity-100={visible}
      class:translate-y-0={visible}
    >
      <h2 class="font-serif text-4xl md:text-6xl text-gold mb-8">
        The Experience
      </h2>
      <p
        class="font-sans text-base md:text-xl text-gray-300 leading-relaxed mb-16 max-w-3xl mx-auto font-light"
      >
        Located in the heart of Saint Louis, Franco creates a gathering place to
        share and savor the finest French cuisine. Our atmosphere strikes the
        perfect balance between elegance and the comfort of home.
      </p>
    </div>

    <!-- Image Grid -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      {#each images as { src, alt, label }, i}
        <div
          class="relative overflow-hidden group h-80 rounded-sm shadow-2xl cursor-pointer transition-all duration-700 ease-out"
          class:opacity-0={!visible}
          class:translate-y-8={!visible}
          class:opacity-100={visible}
          class:translate-y-0={visible}
          style="transition-delay: {(i + 1) * 150}ms"
        >
          <img
            loading="lazy"
            {src}
            {alt}
            class="w-full h-full object-cover transition-transform duration-1000 group-hover:scale-110"
          />
          <div
            class="absolute inset-0 bg-darker/40 flex items-end justify-center pb-8 group-hover:bg-darker/60 transition-all duration-500"
          >
            <span
              class="font-serif text-2xl text-white tracking-widest border-b-2 border-transparent group-hover:border-gold pb-1 transition-all"
            >
              {label}
            </span>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>
