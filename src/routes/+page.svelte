<script lang="ts">
  import { onMount } from "svelte";
  import ImageSlider from "./ImageSlider.svelte";

  let show1 = $state(false);
  let show2 = $state(false);
  let show3 = $state(false);

  let element1: HTMLElement | undefined;
  let element2: HTMLElement | undefined;
  let element3: HTMLElement | undefined;

  onMount(() => {
    if (!element1 || !element2 || !element3) {
      return;
    }

    const observer1 = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          show1 = true;
        }
      },
      { root: null, rootMargin: "-200px 0px", threshold: 0 },
    );

    observer1.observe(element1);

    const observer2 = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) show2 = true;
      },
      { root: null, rootMargin: "-200px 0px", threshold: 0 },
    );

    observer2.observe(element2);

    const observer3 = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) show3 = true;
      },
      { root: null, rootMargin: "-200px 0px", threshold: 0 },
    );

    observer3.observe(element3);

    return () => {
      observer1.disconnect();
      observer2.disconnect();
      observer3.disconnect();
    };
  });
</script>

<svelte:head>
  <title>Valor and Unity Crew</title>
</svelte:head>

<!-- <ImageSlider /> -->

<ul>
  <li
    bind:this={element1}
    class="flex items-center justify-center pt-8 md:p-10 lg:p-12"
  >
    <div
      class="md:bg-[#2A4AA2] md:text-white overflow-hidden md:rounded-3xl md:drop-shadow-xl flex flex-col lg:flex-row transition duration-300 ease-in-out opacity-0 delay-100 {show1
        ? 'opacity-100 translate-y-0'
        : 'translate-y-18'}"
    >
      <img
        src="/images/callouts/vu-crew.png"
        alt="Valor and Unity Crew Officers"
        class="w-full lg:min-w-[50%] max-h-120 lg:max-h-190 object-cover"
      />

      <div
        class="flex flex-col justify-between gap-10 md:gap-12 p-4 md:p-7 md:py-8"
      >
        <div class="flex flex-col gap-4 md:gap-6">
          <h1
            class="font-semibold text-4xl md:text-5xl lg:text-4xl xl:text-[52px]]"
          >
            Our Mission
          </h1>

          <p
            class="flex flex-col gap-[0.5lh] text-lg md:text-xl lg:text-[22px] leading-snug"
          >
            <span
              >The Valor and Unity Crew is a student-led organization committed
              to raising awareness about veteran issues and supporting student
              veterans throughout Florida.</span
            >

            <span
              >Since our founding, we have successfully hosted many events that
              brought community leaders, teachers, and students together to
              empower veterans.</span
            >

            <span
              >We firmly believe in the cultivation of respect for sacrifice,
              service, and discipline by fostering unity between students and
              veterans.</span
            >
          </p>
        </div>

        <a
          href="/events"
          class="flex gap-2 text-lg xl:text-xl items-center justify-center border-2 border-black md:border-white w-full rounded-lg p-2 bg-white/5 hover:bg-white/15 transition-colors"
          >Learn More <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="2"
            stroke="currentColor"
            class="size-5"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M13.5 4.5 21 12m0 0-7.5 7.5M21 12H3"
            />
          </svg>
        </a>
      </div>
    </div>
  </li>

  <li
    bind:this={element2}
    class="flex items-center justify-center md:p-10 pt-8 lg:p-12"
  >
    <div
      class="md:bg-[#E63A32] md:text-white overflow-hidden md:rounded-3xl md:drop-shadow-xl flex flex-col lg:flex-row-reverse transition duration-300 ease-in-out opacity-0 delay-100 {show2
        ? 'opacity-100 translate-y-0'
        : 'translate-y-18'}"
    >
      <img
        src="/images/callouts/vet-salute.png"
        alt="Veteran's Salute"
        class="w-full lg:min-w-[50%] max-h-120 lg:max-h-190 object-cover"
      />

      <div
        class="flex flex-col justify-between gap-10 md:gap-12 p-4 md:p-7 md:py-8"
      >
        <div class="flex flex-col gap-4 md:gap-6">
          <h1
            class="font-semibold text-4xl md:text-5xl lg:text-4xl xl:text-[52px]"
          >
            Our Vision
          </h1>

          <p
            class="flex flex-col gap-[0.5lh] text-lg md:text-xl lg:text-[22px] leading-snug"
          >
            <span>
              The vision behind the Valor and Unity Crew is to consistently
              create events where military branches, university recruiters,
              veterans, students, and families can come out and engage with
              their community.
            </span>

            <span
              >The motive for our events is to raise awareness on the major
              issues that plague the veteran community, further the education of
              the community on these issues, and a demonstration of all
              post-secondary options for families.</span
            >
          </p>
        </div>

        <a
          href="/donate"
          class="flex gap-2 text-lg xl:text-xl items-center justify-center border-2 border-black md:border-white w-full rounded-lg p-2 bg-white/5 hover:bg-white/15 transition-colors"
          >Support Us <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="2"
            stroke="currentColor"
            class="size-5"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M13.5 4.5 21 12m0 0-7.5 7.5M21 12H3"
            />
          </svg>
        </a>
      </div>
    </div>
  </li>

  <li
    bind:this={element3}
    class="flex items-center justify-center md:p-10 pt-8 lg:p-12"
  >
    <div
      class="md:bg-[#132C72] md:text-white overflow-hidden md:rounded-3xl md:drop-shadow-xl flex flex-col lg:flex-row transition duration-300 ease-in-out opacity-0 delay-100 {show3
        ? 'opacity-100 translate-y-0'
        : 'translate-y-18'}"
    >
      <img
        src="/images/callouts/flags.png"
        alt="Collection of American Flags"
        class="w-full lg:min-w-[50%] max-h-120 lg:max-h-190 object-cover"
      />

      <div
        class="flex flex-col justify-between gap-10 md:gap-12 p-4 md:p-7 md:py-8"
      >
        <div class="flex flex-col gap-4 md:gap-6">
          <h1
            class="font-semibold text-4xl md:text-5xl lg:text-4xl xl:text-[52px]"
          >
            Achieving Our Mission
          </h1>

          <p
            class="flex flex-col gap-[0.5lh] text-lg md:text-xl lg:text-[22px] leading-snug"
          >
            <span>
              The Valor and Unity Crew will achieve its mission through various
              means, including the acquisition of staff, fundraising for events,
              and the participation of important community figures such as
              veterans, speakers, and local institution leaders.
            </span>

            <span>
              Community outreach efforts will utilize social media, radio shows,
              talk shows, and TV stations.
            </span>

            <span>
              Necessary security measures will be arranged by contacting
              relevant companies.</span
            >
          </p>
        </div>

        <a
          href="/events"
          class="flex gap-2 text-lg xl:text-xl items-center justify-center border-2 border-black md:border-white w-full rounded-lg p-2 bg-white/5 hover:bg-white/15 transition-colors"
          >View Our Events <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="2"
            stroke="currentColor"
            class="size-5"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M13.5 4.5 21 12m0 0-7.5 7.5M21 12H3"
            />
          </svg>
        </a>
      </div>
    </div>
  </li>
</ul>

<div class="flex flex-col lg:flex-row">
  <img
    src="/images/quote/American Flag.png"
    alt=""
    class="object-cover max-h-85 lg:max-h-full lg:min-h-full lg:max-w-[30%]"
  />
  <div
    class="flex-1 flex flex-col justify-between px-9 py-10 gap-8 bg-[#223F8F] text-white"
  >
    <blockquote
      class="font-quote font-bold italic leading-[1.15] text-4xl md:text-5xl lg:text-4xl xl:text-5xl"
    >
      “Through unity of action we can be a veritable colossus in support of
      peace.”
    </blockquote>

    <cite class="not-italic text-xl xl:text-2xl"
      >— President Dwight D. Eisenhower.</cite
    >
  </div>
  <img
    src="/images/quote/Soldier Standing.png"
    alt=""
    class="object-cover max-h-85 lg:max-h-full lg:min-h-full lg:max-w-[30%]"
  />
</div>
