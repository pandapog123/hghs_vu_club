<script lang="ts">
  import { showOverlay } from "$lib/stores/overlay";
  import { onMount } from "svelte";

  let header: HTMLElement | undefined;
  let changeHeaderColor = $state(false);

  onMount(() => {
    if (!header) return;

    let observer = new IntersectionObserver(([entry]) => {
      changeHeaderColor = !entry.isIntersecting;
    });

    observer.observe(header);

    return () => observer.disconnect();
  });
</script>

<div bind:this={header}></div>

<header
  class="flex justify-between items-center p-6 sm:p-12 sm:py-10 sticky top-0 z-30 transition-colors duration-300 ease-in-out {changeHeaderColor
    ? 'bg-[#d7e2ff]'
    : 'bg-white'}"
>
  <a href="/">
    <h1 class="text-2xl sm:text-3xl lg:text-4xl font-medium">
      Valor and Unity Crew
    </h1>
  </a>

  <nav class="flex items-center">
    <ul class="hidden md:flex gap-4 text-xl">
      <a
        href="/events"
        class="relative inline-block
          after:absolute after:left-0 after:bottom-0
          after:h-0.5 after:w-full
          after:origin-left after:scale-x-0
          after:transition-transform after:duration-300
          after:bg-black after:ease hover:after:scale-x-100"
      >
        <li>Events</li>
      </a>
      <a
        href="/volunteer"
        class="relative inline-block
          after:absolute after:left-0 after:bottom-0
          after:h-0.5 after:w-full
          after:origin-left after:scale-x-0
          after:transition-transform after:duration-300
          after:bg-black after:ease hover:after:scale-x-100"
      >
        <li>Volunteer</li>
      </a>
      <a
        href="/donate"
        class="relative inline-block
          after:absolute after:left-0 after:bottom-0
          after:h-0.5 after:w-full
          after:origin-left after:scale-x-0
          after:transition-transform after:duration-300
          after:bg-black after:ease hover:after:scale-x-100"
      >
        <li>Donate</li>
      </a>
      <a
        href="/contact"
        class="relative inline-block
          after:absolute after:left-0 after:bottom-0
          after:h-0.5 after:w-full
          after:origin-left after:scale-x-0
          after:transition-transform after:duration-300
          after:bg-black after:ease hover:after:scale-x-100"
      >
        <li>Contact</li>
      </a>
    </ul>

    <button
      class="md:hidden"
      onclick={() => {
        $showOverlay = true;
      }}
      ><svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="2"
        stroke="currentColor"
        class="size-9"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
        />
      </svg>
    </button>
  </nav>
</header>
