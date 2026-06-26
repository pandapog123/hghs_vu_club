<script lang="ts">
  import { showOverlay } from "$lib/stores/overlay";
  import { fade, fly } from "svelte/transition";
  import Header from "./Header.svelte";
  import "./layout.css";
  import { cubicIn, cubicInOut, cubicOut } from "svelte/easing";
  import Footer from "./Footer.svelte";

  let { children } = $props();

  let bodyRef: HTMLBodyElement | undefined;

  $effect(() => {
    if (!bodyRef) return;

    if ($showOverlay) {
      bodyRef.classList += "unscroll";
    } else {
      bodyRef.classList.remove("unscroll");
    }
  });
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Manrope:wght@200..800&family=Playfair+Display:ital,wght@0,400..900;1,400..900&display=swap"
    rel="stylesheet"
  />
</svelte:head>

<svelte:body bind:this={bodyRef} />

<div inert={$showOverlay} class="bg-white">
  <Header />

  {@render children()}

  <Footer />
</div>

{#if $showOverlay}
  <div
    inert={!$showOverlay}
    class="fixed top-0 left-0 w-screen h-screen bg-black/60 overflow-hidden z-50"
    in:fade={{ duration: 250 }}
    out:fade={{ delay: 50, duration: 250 }}
  >
    <nav
      class="fixed top-16 w-full h-[calc(100vh-4rem)] rounded-t-4xl p-8 bg-white flex justify-between items-start"
      in:fly={{
        delay: 50,
        duration: 250,
        y: "100%",
        opacity: 1,
        easing: cubicOut,
      }}
      out:fly={{
        // delay: 50,
        duration: 250,
        y: "100%",
        opacity: 1,
        easing: cubicIn,
      }}
    >
      <ul
        class="font-medium text-3xl sm:text-4xl flex flex-col gap-4 leading-none mt-2"
      >
        <a
          href="/"
          onclick={() => {
            $showOverlay = false;
          }}
        >
          <li>Home</li>
        </a>
        <a
          href="/events"
          onclick={() => {
            $showOverlay = false;
          }}
        >
          <li>Events</li>
        </a>
        <a
          href="/volunteer"
          onclick={() => {
            $showOverlay = false;
          }}
        >
          <li>Volunteer</li>
        </a>
        <a
          href="/donate"
          onclick={() => {
            $showOverlay = false;
          }}
        >
          <li>Donate</li>
        </a>
        <a
          href="/contact"
          onclick={() => {
            $showOverlay = false;
          }}
        >
          <li>Contact</li>
        </a>
      </ul>

      <button
        class="h-min"
        onclick={() => {
          $showOverlay = false;
        }}
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="2"
          stroke="currentColor"
          class="size-10 sm:size-12"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6 18 18 6M6 6l12 12"
          />
        </svg>
      </button>
    </nav>
  </div>
{/if}
