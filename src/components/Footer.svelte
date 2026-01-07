<script lang="ts">
  const socialLinks = [
    { href: "#", icon: "fa-brands fa-instagram", label: "Instagram" },
    { href: "#", icon: "fa-brands fa-facebook-f", label: "Facebook" },
    {
      href: "mailto:franco@eatatfranco.com",
      icon: "fa-solid fa-envelope",
      label: "Email",
    },
  ];

  const currentYear = new Date().getFullYear();
</script>

<footer class="py-16 px-4 bg-wine-pattern bg-cover bg-center relative">
  <!-- Overlay -->
  <div class="absolute inset-0 bg-darker/90"></div>

  <div class="relative z-10 max-w-6xl mx-auto text-center">
    <!-- Logo -->
    <div class="mb-8">
      <a
        href="/"
        class="font-serif text-3xl md:text-4xl font-bold tracking-widest uppercase text-white hover:text-gold transition-colors"
      >
        Franco<span class="text-gold">.</span>
      </a>
    </div>

    <!-- Quick Links -->
    <div class="flex flex-wrap justify-center gap-6 md:gap-10 mb-10">
      <a
        href="/"
        class="font-sans text-xs uppercase tracking-widest text-gray-400 hover:text-gold transition-colors"
        >Home</a
      >
      <a
        href="/dinner-menu"
        class="font-sans text-xs uppercase tracking-widest text-gray-400 hover:text-gold transition-colors"
        >Menu</a
      >
      <a
        href="/about"
        class="font-sans text-xs uppercase tracking-widest text-gray-400 hover:text-gold transition-colors"
        >About</a
      >
      <a
        href="/private-events"
        class="font-sans text-xs uppercase tracking-widest text-gray-400 hover:text-gold transition-colors"
        >Private Events</a
      >
      <a
        href="/contact-us"
        class="font-sans text-xs uppercase tracking-widest text-gray-400 hover:text-gold transition-colors"
        >Contact</a
      >
    </div>

    <!-- Social Links -->
    <div class="flex justify-center gap-10 text-2xl text-white/70 mb-10">
      {#each socialLinks as { href, icon, label }}
        <a
          {href}
          class="hover:text-gold hover:scale-110 transition-all duration-300"
          aria-label={label}
        >
          <i class={icon}></i>
        </a>
      {/each}
    </div>

    <!-- Address -->
    <p class="font-sans text-sm text-gray-400 mb-6">
      1535 South Eighth St. • St. Louis, Missouri 63104 • 314.436.2500
    </p>

    <!-- Copyright -->
    <p class="text-[10px] text-gray-500 uppercase tracking-widest">
      © {currentYear} Franco. All Rights Reserved.
    </p>
  </div>
</footer>
