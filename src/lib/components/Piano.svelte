<script lang="ts">
  import type { Entry } from "$lib/types";
  import { page } from "$app/stores";
  import * as Tone from "tone";
  import { onMount } from "svelte";
  import { entries } from "$lib/stores";
  import { gsap } from "gsap";

  import C1 from "$lib/audio/C1.wav";
  import C2 from "$lib/audio/C2.wav";
  import C3 from "$lib/audio/C3.wav";
  import C4 from "$lib/audio/C4.wav";
  import C5 from "$lib/audio/C5.wav";
  import C6 from "$lib/audio/C6.wav";

  import G1 from "$lib/audio/G1.wav";
  import G2 from "$lib/audio/G2.wav";
  import G3 from "$lib/audio/G3.wav";
  import G4 from "$lib/audio/G4.wav";
  import G5 from "$lib/audio/G5.wav";

  import B1 from "$lib/audio/B1.wav";
  import B2 from "$lib/audio/B2.wav";
  import B3 from "$lib/audio/B3.wav";
  import B4 from "$lib/audio/B4.wav";
  import B5 from "$lib/audio/B5.wav";
  import { scale } from "svelte/transition";

  gsap.registerPlugin();

  let notesInOrder = [
    "B7",
    "A7",
    "G7",
    "F7",
    "E7",
    "D7",
    "C7",
    "B6",
    "A6",
    "G6",
    "F6",
    "E6",
    "D6",
    "C6",
    "B5",
    "A5",
    "G5",
    "F5",
    "E5",
    "D5",
    "C5",
    "B4",
    "A4",
    "G4",
    "F4",
    "E4",
    "D4",
    "C4",
    "B3",
    "A3",
    "G3",
    "F3",
    "E3",
    "D3",
    "C3",
    "B2",
    "A2",
    "G2",
    "F2",
    "E2",
    "D2",
    "C2",
    "B1",
    "A1",
    "G1",
    "F1",
    "E1",
    "D1",
    "C1",
    "B0",
    "A0",
  ];

  let blackNotesInOrder = [
    "Bb7",
    "Ab7",
    "Gb7",
    "",
    "Eb7",
    "Db7",
    "",
    "Bb6",
    "Ab6",
    "Gb6",
    "",
    "Eb6",
    "Db6",
    "",
    "Bb5",
    "Ab5",
    "Gb5",
    "",
    "Eb5",
    "Db5",
    "",
    "Bb4",
    "Ab4",
    "Gb4",
    "",
    "Eb4",
    "Db4",
    "",
    "Bb3",
    "Ab3",
    "Gb3",
    "",
    "Eb3",
    "Db3",
    "",
    "Bb2",
    "Ab2",
    "Gb2",
    "",
    "Eb2",
    "Db2",
    "",
    "Bb1",
    "Ab1",
    "Gb1",
    "",
    "Eb1",
    "Db1",
    "",
    "Bb0",
    "Ab0",
  ];

  let notesInOrderReverse = [
    "C1",
    "D1",
    "E1",
    "F1",
    "G1",
    "A1",
    "B1",
    "C2",
    "D2",
    "E2",
    "F2",
    "G2",
    "A2",
    "B2",
    "C3",
    "D3",
    "E3",
    "F3",
    "G3",
    "A3",
    "B3",
    "C4",
    "D4",
    "E4",
    "F4",
    "G4",
    "A4",
    "B4",
    "C5",
    "D5",
    "E5",
    "F5",
    "G5",
    "A5",
    "B5",
    "C6",
    "D6",
    "E6",
    "F6",
    "G6",
    "A6",
    "B6",
    "C7",
    "D7",
    "E7",
    "F7",
    "G7",
    "A7",
    "B7",
    "C8",
    "D7",
  ];

  let blackNotesInOrderReverse = [
    "Db1",
    "Eb1",
    "",
    "Gb1",
    "Ab1",
    "Bb1",
    "",
    "Db2",
    "Eb2",
    "",
    "Gb2",
    "Ab2",
    "Bb2",
    "",
    "Db3",
    "Eb3",
    "",
    "Gb3",
    "Ab3",
    "Bb3",
    "",
    "Db4",
    "Eb4",
    "",
    "Gb4",
    "Ab4",
    "Bb4",
    "",
    "Db5",
    "Eb5",
    "",
    "Gb5",
    "Ab5",
    "Bb5",
    "",
    "Db6",
    "Eb6",
    "",
    "Gb6",
    "Ab6",
    "Bb6",
    "",
    "Db7",
    "Eb7",
    "",
    "Gb7",
    "Ab7",
    "Bb7",
    "",
    "Db1",
    "",
  ];

  let synth: any;
  const playWhiteKey = (idx: number) => {
    synth.triggerAttackRelease(notesInOrder[idx % notesInOrder.length], "2n");
  };
  const playBlackKey = (idx: number) => {
    synth.triggerAttackRelease(
      blackNotesInOrder[idx % blackNotesInOrder.length],
      "2n"
    );
  };

  onMount(() => {
    const vol = new Tone.Volume(-8).toDestination();
    synth = new Tone.Sampler({
      urls: {
        C1,
        C2,
        C3,
        C4,
        C5,
        C6,
        G1,
        G2,
        G3,
        G4,
        G5,
        B1,
        B2,
        B3,
        B4,
        B5,
      },
    }).connect(vol);
  });
</script>

{#each $entries as entry, idx}
  <div class="key-container" id="entry-{idx}">
    <a
      href="/{entry.slug}"
      on:click={() => {
        playWhiteKey(idx);
      }}
    >
      <div class="entryName">
        {entry.name}
      </div>
    </a>
    <div
      class=" 
			{entry.slug === $page.params.name ? 'text-black' : 'text-grey4'}
      right-0 top-0 w-8 h-20 absolute text-xs tracking-wide flex justify-center items-center rounded-[10rem]"
    >
      {notesInOrder[idx % notesInOrder.length]}
    </div>
    <div
      class="black-key"
      on:click={() => {
        playBlackKey(idx);
      }}
      on:keydown={(event) => {
        if (event.key === "Enter") {
          playBlackKey(idx);
        }
      }}
      role="button"
      tabindex="0"
      on:mouseenter={(event) => {
        // console.log(event.target);
        // gsap.to(event.target, {
        //   // attr: { y1: "1.2" },
        //   scale: 1.1,
        //   duration: 0.2,
        // });
      }}
    >
      <!-- <svg
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        width="232"
        height="50.027"
        viewBox="0 0 232 50.027"
      >
        <defs>
          <linearGradient
            id="linear-gradient"
            x1="1.347"
            y1="0.925"
            x2="0.318"
            y2="1.479"
            gradientUnits="objectBoundingBox"
          >
            <stop offset="0" />
            <stop offset="0.499" stop-color="#434343" />
            <stop offset="1" stop-color="#0c0c0c" />
          </linearGradient>
        </defs>
        <g id="Group_2" data-name="Group 2" transform="translate(1649 -3966)">
          <path
            id="Path_63"
            data-name="Path 63"
            d="M0,0H223.245V41.9H0Z"
            transform="translate(-1649 3966)"
            fill="url(#linear-gradient)"
          />
          <path
            id="Path_61"
            data-name="Path 61"
            d="M-1317,4116.272V4075a13.4,13.4,0,0,1,5.628,1.876,10.709,10.709,0,0,1,3.127,4.377v37.521a6.454,6.454,0,0,1-.625,2.5,7.888,7.888,0,0,1-1.646,1.653Z"
            transform="translate(-108.755 -109)"
            fill="#706969"
          />
          <path
            id="Path_62"
            data-name="Path 62"
            d="M-1673,4303.625l223.245-.625,6.531,6.58a17.844,17.844,0,0,1-2.154,1.549,7.4,7.4,0,0,1-3.127.625H-1673Z"
            transform="translate(24 -295.728)"
            fill="#545454"
          />
        </g>
      </svg> -->
    </div>
  </div>
{/each}

<style lang="scss">
  .key-container {
    @apply -mt-[1px] relative bg-[#D7D1C6] -ml-1;
    /* border: 1px solid #707070; */

    border-left: 1px solid #bbb;
    border-bottom: 1px solid #bbb;
    border-top: 1px solid #d7d1c6;

    border-radius: 5px;
    box-shadow:
      -1px 0 0 rgba(255, 255, 255, 0.8) inset,
      0 0 5px #ccc inset,
      0 0 3px rgba(0, 0, 0, 0.2);
    background: linear-gradient(to bottom, #d7d1c6 0%, #fff 100%);
    transition: all 0.1s ease-in-out;

    &:active {
      border-top: 1px solid #777;
      border-left: 1px solid #999;
      border-bottom: 1px solid #999;
      box-shadow:
        2px 0 3px rgba(0, 0, 0, 0.1) inset,
        -5px 5px 20px rgba(0, 0, 0, 0.2) inset,
        0 0 3px rgba(0, 0, 0, 0.2);
      background: linear-gradient(to left, #d7d1c6 0%, #e9e9e9 100%);
    }

    &:nth-child(7n + 4),
    &:nth-child(7n),
    &:last-child {
      .black-key {
        display: none;
      }
    }

    .entryName {
      @apply h-20 justify-end pr-8 relative flex items-center rounded-r-md text-3xl;
      font-family: Eurostile;
      font-weight: 600;
    }

    .black-key {
      @apply h-10 absolute top-[3.75rem] w-[12.5vw] z-10 rounded-r-md flex;
      svg {
        @apply h-full w-full -ml-1;
      }

      border: 1px solid #000;
      border-radius: 0 3px 3px 3px;
      box-shadow:
        -1px -1px 2px rgba(255, 255, 255, 0.2) inset,
        0 -5px 2px 3px rgba(0, 0, 0, 0.6) inset,
        0 2px 4px rgba(0, 0, 0, 0.5);
      background: linear-gradient(45deg, #222 0%, #555 100%);
      transition: all 0.1s ease-in-out;

      &:active {
        box-shadow:
          -1px -1px 2px rgba(255, 255, 255, 0.2) inset,
          0 -2px 2px 3px rgba(0, 0, 0, 0.6) inset,
          0 1px 2px rgba(0, 0, 0, 0.5);
        background: linear-gradient(to right, #444 0%, #222 100%);
      }
    }
  }
</style>
