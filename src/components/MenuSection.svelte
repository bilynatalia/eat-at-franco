<script lang="ts">
  import { onMount } from "svelte";

  interface MenuItem {
    name: string;
    price: string;
    description: string;
  }

  interface MenuCategory {
    name: string;
    note?: string;
    items: MenuItem[];
  }

  const menuCategories: Record<string, MenuCategory> = {
    "small-plates": {
      name: "Small Plates",
      items: [
        {
          name: "Brie-Walnut Gougeres",
          price: "$8",
          description: "Spinach, raito sauce",
        },
        {
          name: "Pommes Frites",
          price: "$6",
          description: "Black pepper, sea salt, mayonnaise",
        },
        {
          name: "Escargots",
          price: "$10",
          description:
            "In shell, chorizo, caramelized onion, tomato-sherry broth",
        },
        {
          name: "Seared Scallops",
          price: "$18",
          description: "Corn, andouille, baby potatoes, crawfish, nantua sauce",
        },
        {
          name: "Duo of Tartare",
          price: "$13",
          description: "Beef tenderloin & tuna tartare, gaufrettes",
        },
        {
          name: "Cheese Flight",
          price: "$15",
          description: "Grapes, nuts, grain mustard (Selection of 3)",
        },
      ],
    },
    "fruits-de-mer": {
      name: "Fruits De Mer",
      note: "Served with champagne-mignonette, cocktail sauce, and lemon",
      items: [
        {
          name: "Grand Plateau",
          price: "$40",
          description: "Scallop, shrimp, oysters, clams, octopus, mussel",
        },
        {
          name: "Oysters",
          price: "MKT",
          description: "Half Shell, Daily Selection",
        },
        { name: "Shrimp Cocktail", price: "$2 ea", description: "" },
        { name: "Trout Caviar", price: "$30", description: "2 oz jar" },
      ],
    },
    entrees: {
      name: "Entrées",
      items: [
        {
          name: "Grilled Hereford Strip",
          price: "$30",
          description: "Pommes frites, chateaubriand sauce, roast bone marrow",
        },
        {
          name: "Oven Roasted Chicken",
          price: "$24",
          description:
            "Black truffle-grain mustard stuffed skin, brown ale sauce",
        },
        {
          name: "Cochon Crépinette",
          price: "$27",
          description: "Pork jus, braised red cabbage, dauphinoise potatoes",
        },
        {
          name: "Loup de Mer",
          price: "$32",
          description: "Stuffed with shellfish boudin, blanquette of corn",
        },
        {
          name: "Seafood Stew",
          price: "$25",
          description: "Squid, shrimp, octopus, clam, mussel, chorizo, fumet",
        },
        {
          name: "Provençal Lamb Shank",
          price: "$32",
          description: "Wild mushroom and pearl barley ragout, lamb confit",
        },
      ],
    },
    desserts: {
      name: "Desserts",
      items: [
        {
          name: "Chocolate Pot de Crème",
          price: "$9",
          description:
            "Nutella crème chantilly, financier cake, pistachio ice cream",
        },
        {
          name: "Apple Tarte Tatin",
          price: "$7",
          description: "Vanilla ice cream",
        },
        {
          name: "Mignardises",
          price: "$8",
          description: "Assortment of petit fours (5 pc)",
        },
        { name: "Crème Brulée", price: "$6", description: "Tahitian Vanilla" },
      ],
    },
  };

  const categoryKeys = Object.keys(menuCategories);
  let activeCategory = "small-plates";
  let visibleItems: boolean[] = [];

  function filterMenu(category: string) {
    activeCategory = category;
    visibleItems = [];
    setTimeout(() => {
      const items = menuCategories[category].items;
      items.forEach((_, i) => {
        setTimeout(() => {
          visibleItems = [...visibleItems, true];
        }, i * 100);
      });
    }, 50);
  }

  onMount(() => {
    filterMenu("small-plates");
  });
</script>

<section
  id="menu"
  class="min-h-screen bg-menu-pattern bg-cover bg-fixed relative py-24 px-4 md:px-16 lg:px-24"
>
  <div class="max-w-7xl mx-auto">
    <!-- Section Header -->
    <div class="text-center mb-16">
      <h2 class="font-serif text-4xl md:text-6xl text-gold mb-4">Our Menu</h2>
      <p class="font-sans text-sm md:text-lg text-gray-300 italic font-light">
        Classic French techniques, locally sourced ingredients.
      </p>
    </div>

    <!-- Menu Tabs -->
    <div
      class="flex overflow-x-auto md:justify-center gap-8 md:gap-12 mb-16 pb-4 md:pb-0 no-scrollbar whitespace-nowrap border-b border-gray-700/50 md:border-none px-4"
    >
      {#each categoryKeys as key}
        <button
          on:click={() => filterMenu(key)}
          class="menu-tab font-serif text-lg md:text-2xl pb-2 focus:outline-none transition-colors"
          class:active={activeCategory === key}
          class:text-white={activeCategory === key}
          class:text-gray-400={activeCategory !== key}
        >
          {menuCategories[key].name}
        </button>
      {/each}
    </div>

    <!-- Menu Items -->
    <div class="min-h-[500px]">
      {#if menuCategories[activeCategory].note}
        <div class="text-center mb-12">
          <p
            class="text-gold italic text-sm md:text-base border border-gold/30 inline-block px-6 py-2 rounded-full"
          >
            {menuCategories[activeCategory].note}
          </p>
        </div>
      {/if}

      <div class="grid md:grid-cols-2 gap-x-20 gap-y-10">
        {#each menuCategories[activeCategory].items as item, i}
          <div
            class="border-b border-gray-700/30 pb-4 group transition-all duration-500"
            class:opacity-0={!visibleItems[i]}
            class:opacity-100={visibleItems[i]}
            class:translate-y-4={!visibleItems[i]}
            class:translate-y-0={visibleItems[i]}
          >
            <div class="flex justify-between items-baseline mb-2">
              <h3
                class="font-serif text-xl md:text-2xl text-white group-hover:text-gold transition-colors"
              >
                {item.name}
              </h3>
              <span class="font-serif text-gold text-xl">{item.price}</span>
            </div>
            {#if item.description}
              <p class="text-sm text-gray-400 italic">{item.description}</p>
            {/if}
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>
