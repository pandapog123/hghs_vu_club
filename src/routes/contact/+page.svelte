<script lang="ts">
  import { fade, fly, scale } from "svelte/transition";
  import { cubicOut } from "svelte/easing";

  const contactEmail = "president@hghsvucrew.com";

  let sending = $state(false);
  let showPopup = $state(false);
  let errorMessage = $state("");

  async function submitContact(event: SubmitEvent) {
    event.preventDefault();

    sending = true;
    errorMessage = "";

    const form = event.currentTarget as HTMLFormElement;
    const formData = new FormData(form);

    formData.append("_subject", "New message from Valor and Unity Crew website");
    formData.append("_template", "table");
    formData.append("_captcha", "false");

    try {
      const response = await fetch(`https://formsubmit.co/ajax/${contactEmail}`, {
        method: "POST",
        body: formData,
        headers: {
          Accept: "application/json",
        },
      });

      const result = await response.json();

      if (!response.ok || !result.success) {
        errorMessage = "Something went wrong. Please try again.";
        return;
      }

      form.reset();
      showPopup = true;
    } catch (error) {
      errorMessage = "Something went wrong. Please try again.";
    } finally {
      sending = false;
    }
  }
</script>

<svelte:head>
  <title>Contact - Valor and Unity Crew</title>
</svelte:head>

<section
  class="bg-white px-4 py-10 md:px-8 lg:px-10 lg:py-12"
  in:fade={{ duration: 300 }}
>
  <div class="mx-auto max-w-7xl">
    <h1
      class="text-5xl font-semibold leading-tight text-black md:text-6xl"
      in:fly={{ y: 18, duration: 450, easing: cubicOut }}
    >
      Contact Us
    </h1>

    <p
      class="mt-3 max-w-5xl text-base leading-snug text-black md:text-lg"
      in:fly={{ y: 18, duration: 450, delay: 100, easing: cubicOut }}
    >
      Thank you for your interest in the Valor and Unity Crew! We are happy to
      answer any questions you might have. Leave your contact info and we will
      reach out as soon as we can!
    </p>

    <hr
      class="mt-6 border-gray-200"
      in:fade={{ duration: 450, delay: 180 }}
    />

    <form
      onsubmit={submitContact}
      class="mt-4 flex flex-col gap-4"
      in:fly={{ y: 22, duration: 500, delay: 220, easing: cubicOut }}
    >
      <input type="text" name="_honey" style="display: none" />

      <div class="grid gap-3 md:grid-cols-3">
        <label
          class="flex flex-col gap-1 text-base text-black"
          in:fly={{ y: 18, duration: 400, delay: 280, easing: cubicOut }}
        >
          First name (required)
          <input
            name="First Name"
            required
            type="text"
            placeholder="Enter your first name"
            class="rounded-lg border border-gray-300 px-3 py-2 text-sm text-black outline-none transition focus:border-[#3D56B2]"
          />
        </label>

        <label
          class="flex flex-col gap-1 text-base text-black"
          in:fly={{ y: 18, duration: 400, delay: 340, easing: cubicOut }}
        >
          Last name (required)
          <input
            name="Last Name"
            required
            type="text"
            placeholder="Enter your last name"
            class="rounded-lg border border-gray-300 px-3 py-2 text-sm text-black outline-none transition focus:border-[#3D56B2]"
          />
        </label>

        <label
          class="flex flex-col gap-1 text-base text-black"
          in:fly={{ y: 18, duration: 400, delay: 400, easing: cubicOut }}
        >
          Email (required)
          <input
            name="email"
            required
            type="email"
            placeholder="Enter your e-mail address"
            class="rounded-lg border border-gray-300 px-3 py-2 text-sm text-black outline-none transition focus:border-[#3D56B2]"
          />
        </label>
      </div>

      <label
        class="flex flex-col gap-1 text-base text-black"
        in:fly={{ y: 18, duration: 400, delay: 460, easing: cubicOut }}
      >
        Your message
        <textarea
          name="Message"
          required
          rows="6"
          placeholder="Enter your message"
          class="resize-none rounded-lg border border-gray-300 px-3 py-2 text-sm text-black outline-none transition focus:border-[#3D56B2]"
        ></textarea>
      </label>

      {#if errorMessage}
        <div
          class="rounded-lg border border-red-300 bg-red-50 px-4 py-3 text-sm text-red-700"
          transition:fly={{ y: 12, duration: 250, easing: cubicOut }}
        >
          {errorMessage}
        </div>
      {/if}

      <div
        class="flex justify-end"
        in:fly={{ y: 18, duration: 400, delay: 520, easing: cubicOut }}
      >
        <button
          type="submit"
          disabled={sending}
          class="flex cursor-pointer items-center justify-center gap-1 rounded-lg bg-[#3D56B2] px-4 py-2 text-sm text-white transition hover:bg-[#2A4AA2] disabled:cursor-not-allowed disabled:opacity-60"
        >
          {sending ? "Sending..." : "Send Message"}

          {#if !sending}
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="2"
              stroke="currentColor"
              class="size-4"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M13.5 4.5 21 12m0 0-7.5 7.5M21 12H3"
              />
            </svg>
          {/if}
        </button>
      </div>
    </form>
  </div>
</section>

{#if showPopup}
  <div
    class="fixed inset-0 z-50 flex items-center justify-center bg-black/40 px-4"
    role="dialog"
    aria-modal="true"
    transition:fade={{ duration: 150 }}
  >
    <div
      class="w-full max-w-md rounded-3xl bg-white p-8 text-center shadow-2xl will-change-transform"
      transition:scale={{
        duration: 180,
        start: 0.96,
        opacity: 0,
        easing: cubicOut,
      }}
    >
      <div
        class="mx-auto flex size-16 items-center justify-center rounded-full bg-[#3D56B2] text-white"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="2.5"
          stroke="currentColor"
          class="size-8"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="m4.5 12.75 6 6 9-13.5"
          />
        </svg>
      </div>

      <h2 class="mt-5 text-3xl font-semibold text-[#132C72]">
        Message Sent!
      </h2>

      <p class="mt-3 text-base leading-snug text-gray-700">
        Thank you for reaching out. We received your message and will get back
        to you as soon as possible.
      </p>

      <button
        type="button"
        onclick={() => {
          showPopup = false;
        }}
        class="mt-7 cursor-pointer rounded-lg bg-[#3D56B2] px-6 py-2 text-sm font-medium text-white transition hover:bg-[#2A4AA2]"
      >
        Close
      </button>
    </div>
  </div>
{/if}