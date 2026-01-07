<script lang="ts">
  import { onMount } from 'svelte';

  let scrolled = false;
  let mobileMenuOpen = false;

  const navLinks = [
    { href: '/', label: 'Home' },
    { href: '/dinner-menu', label: 'Dinner' },
    { href: '/about', label: 'About' },
    { href: '/private-events', label: 'Private Events' },
    { href: '/contact-us', label: 'Contact Us' },
  ];

  function toggleMobileMenu() {
    mobileMenuOpen = !mobileMenuOpen;
    if (mobileMenuOpen) {
      document.body.style.overflow = 'hidden';
    } else {
      document.body.style.overflow = 'auto';
    }
  }

  function closeMobileMenu() {
    mobileMenuOpen = false;
    document.body.style.overflow = 'auto';
  }

  onMount(() => {
    const handleScroll = () => {
      scrolled = window.scrollY > 50;
    };

    window.addEventListener('scroll', handleScroll, { passive: true });
    return () => window.removeEventListener('scroll', handleScroll);
  });
</script>

<!-- Navigation Bar -->
<nav
  class="fixed w-full z-50 px-6 py-6 md:px-12 md:py-8 flex justify-between items-center text-white transition-all duration-300"
  class:scrolled
>
  <!-- Logo -->
  <div class="logo font-serif text-2xl md:text-3xl font-bold tracking-widest uppercase cursor-pointer hover:text-gold transition-colors">
    <a href="/">Franco<span class="text-gold">.</span></a>
  </div>

  <!-- Mobile Menu Button -->
  <button
    on:click={toggleMobileMenu}
    class="md:hidden text-2xl text-gold focus:outline-none p-2 hover:scale-110 transition-transform"
    aria-label="Open mobile menu"
    aria-expanded={mobileMenuOpen}
  >
    <i class="fa-solid fa-bars"></i>
  </button>

  <!-- Desktop Links -->
  <div class="hidden md:flex gap-8 lg:gap-12">
    {#each navLinks as { href, label }}
      <a
        {href}
        class="font-sans text-xs lg:text-sm font-bold uppercase tracking-widest hover:text-gold transition-colors pb-1 border-b-2 border-transparent hover:border-gold"
      >
        {label}
      </a>
    {/each}
  </div>
</nav>

<!-- Mobile Menu Overlay -->
<div
  class="fixed inset-0 bg-darker/98 backdrop-blur-xl z-40 flex flex-col justify-center items-center gap-8 transition-transform duration-500"
  class:translate-x-full={!mobileMenuOpen}
>
  <button
    on:click={closeMobileMenu}
    class="absolute top-6 right-6 text-3xl text-gold p-4 hover:rotate-90 transition-transform duration-300"
    aria-label="Close mobile menu"
  >
    <i class="fa-solid fa-times"></i>
  </button>
  
  {#each navLinks as { href, label }}
    <a
      {href}
      on:click={closeMobileMenu}
      class="text-3xl font-serif text-white hover:text-gold transition-colors tracking-wider"
    >
      {label}
    </a>
  {/each}
</div>

<style>
  nav.scrolled {
    background-color: rgba(18, 11, 8, 0.95);
    padding-top: 1rem;
    padding-bottom: 1rem;
    backdrop-filter: blur(8px);
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.3);
    border-bottom: 1px solid rgba(197, 160, 89, 0.1);
  }
</style>
