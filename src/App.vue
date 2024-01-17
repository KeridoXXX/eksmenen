<script setup>
import { reactive, ref } from "vue";
import Helements from "./components/Helements.vue";

const logoUrl = "http://localhost:8080/logos/";
let currentTrackIndex = 0;
let showPlayer = false;

const spotifyData = {
  // Hardcoded data from spotify
  "a-perfect-circle": [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/5KDNFlHAdDJ84fhK27c35X?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7gDVjl5fEw2OPAtjbW4LzR?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6CqYhhUPJORx1vvdTNc8jv?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  tool: [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/1lATXTBJDHwawvT1UfxWu3?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6DyywdbmTzlmXBzG9ym7Rt?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6AioOohg4bQZFA4jIYQQ2r?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  terminalist: [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/5vSaktkX5cG6Wi4eDvrtjx?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6Kv1j5Oiohb0vlIdVWcwwN?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/4mgyqyRqwDRmE5TqZZzyQO?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  "led-zeppelin": [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/5CQ30WqJwcep0pYcV4AMNc?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/78lgmZwycJ3nzsdgmPPGNx?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/0hCB0YR03f6AmQaHbwWDe8?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  "the-beatles": [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6dGnYIeXmHdcikdzNNDMm2?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/2EqlS6tkEnglzr7tkKAAYD?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/3BQHpFgAp4l80e1XslIjNI?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  "pink-floyd": [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7rPzEczIS574IgPaiPieS3?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/1HzDhHApjdjXPLHF6GGYhu?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7Fg4jpwpkdkGCvq1rrXnvx?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  queen: [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/5T8EDUDqKcs6OSOwEsfqG7?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/4u7EnebtmKWzUH433cf5Qv?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/5vdp5UmvTsnMEMESIF2Ym7?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  metallica: [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/5sICkBXVmaCQk5aISGR3x1?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/0nLiqZ6A27jJri2VCalIUs?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/2MuWTIM3b0YEAskbeeFE1i?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  acdc: [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/2zYzyRzz6pRmhPzyfMEC8s?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/57bgtoPSgt236HzfBOd8kj?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/08mG3Y1vljYA6bvDt4Wqkj?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  "the-rolling-stones": [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/63T7DJ1AFDD6Bn8VzG6JE8?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7HKez549fwJQDzx3zLjHKC?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/2PzU4IB8Dr6mxV3lHuaG34?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  "guns-n-roses": [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7snQQk1zcKl8gZ92AnueZW?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/0G21yYKMZoHa30cYVi1iA8?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6eN1f9KNmiWEhpE2RhQqB5?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  nirvana: [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/4CeeEOM32jQcH3eN9Q2dGj?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/2RsAajgo0g7bMCHxwH3Sk0?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/11LmqTE2naFULdEP94AUBa?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  "the-who": [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/3qiyyUfYe7CRYLucrPmulD?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/4u9f8hqstB7iITDJNzKhQx?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/0cKk8BKEi7zXbdrYdyqBP5?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  "black-sabbath": [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/3Jnxngdff0lVu2rza1GVx6?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/755bvJDSA3LNcNuFgBT9LK?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6TYQRlRci6AkVrN9a5C7ne?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  "raised-fist": [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/0o700FqVYCvzdCYXxfX92m?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7mHkTOIj2ueTzwTPdoukKE?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6jSlBXOPo6VFW4OAVK3luj?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
  refused: [
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/35iLpqqQg4KrfYAzbvN1vH?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/2yuSLHwPoOoB1zDuXnQnqZ?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
    '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/0C9JzWHcKsyY8AzgCM97h0?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  ],
};

const placeholderBand = [
  // Peter Ulf
  '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/5DTdPD0aduize5qYHtv6S0?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7GGyu5rdwwEIpbhjSKPN5x?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
  '<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/5amJPj4mW0qQxCUu4JjsdF?utm_source=generator" width="100%" height="200" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>',
];

const state = reactive({
  // Declaring reactive state, band for use in template and isDragging for use in functions
  bands: null,
  isDragging: false,
});

const openClick = new Audio("/openclick.mp3"); // SFX
const closeClick = new Audio("/closeclick.mp3"); // SFX
const loadSound = new Audio("/tapeload.mp3"); // SFX

// for "animation" and sfx
function payload() {
  state.isDragging = true;
  console.log(state.isDragging);
  openClick.play();
}
// for "animation" and sfx
function noPayload() {
  state.isDragging = false;
  console.log(state.isDragging);
  closeClick.play();
}

async function getBands() {
  const response = await fetch("http://localhost:8080/bands");
  state.bands = await response.json();
  console.log("data fetched", state.bands);
}

let draggedBand = null; // Declaring draggedBand for use in functions
let currentBand = null; // same ^

function dragStart(event, band) {
  //
  console.log("drag start");
  draggedBand = band; // band specific data is being set? the band param is reffering to the band in the v-for loop
}

function dragEnd(event) {
  console.log("drag end");
}

// event is the drop event
function drop(event) {
  let iframeData;
  // if statement to specify real or fake band
  if (draggedBand.logo.startsWith("https")) {
    iframeData = placeholderBand;
  } else {
    iframeData = spotifyData[draggedBand.slug];
  }

  document.querySelector(".iframe-target").innerHTML = iframeData[0]; // first song

  document.querySelector(".player").classList.remove("hidden"); // show player

  currentBand = draggedBand; // set current band to dragged band - this enables the next and previous buttons to work
  draggedBand = null; //reset
  loadSound.play();
}

function nextTrack() {
  const iframeData = currentBand.logo.startsWith("https")
    ? placeholderBand
    : spotifyData[currentBand.slug]; // determine if real or fake band
  currentTrackIndex = (currentTrackIndex + 1) % 3;
  document.querySelector(".iframe-target").innerHTML =
    iframeData[currentTrackIndex];
}

function previousTrack() {
  const iframeData = currentBand.logo.startsWith("https")
    ? placeholderBand
    : spotifyData[currentBand.slug];
  currentTrackIndex = (currentTrackIndex - 1 + 3) % 3;
  document.querySelector(".iframe-target").innerHTML =
    iframeData[currentTrackIndex];
}

getBands();
</script>

<template>
  <header><Helements></Helements></header>
  <main>
    <div class="grid grid-cols-2 bg-white">
      <div class="grid gap-4 py-4 overflow-scroll h-screen justify-center">
        <div
          class="tape w-80 h-40 rounded-lg border-4 border-black"
          v-for="band in state.bands"
          draggable="true"
          @dragstart="dragStart($event, band)"
          @dragend="dragEnd($event)"
        >
          <div class="toppart">
            <img
              class="object-cover w-full h-24 rounded-t-sm"
              :src="
                band.logo.startsWith('https://')
                  ? band.logo
                  : logoUrl + band.logo
              "
              alt=""
            />
          </div>
          <div class="holes">
            <div class="hole"></div>
            <div class="hole"></div>
          </div>

          <div class="label">
            <p>{{ band.name }}</p>
            <p>{{ band.genre }}</p>
          </div>
        </div>
      </div>
      <div
        class="dropzone flex flex-col items-center"
        @dragover.prevent
        @drop="drop($event)"
      >
        <div class="w-100 h-100 my-4">
          <img
            class="w-80 h-80"
            @dragenter="payload"
            @dragleave="noPayload"
            @drop="noPayload"
            :src="state.isDragging ? '/open.webp' : '/closed.webp'"
            alt=""
          />
        </div>
        <div class="iframe-target"></div>
        <div class="player hidden flex justify-between">
          <button class="toggle-song bg-orange-600" @click="previousTrack">
            Previous
          </button>
          <button class="toggle-song bg-orange-600" @click="nextTrack">
            Next
          </button>
        </div>
      </div>
    </div>
  </main>
  <footer></footer>
</template>

<style scoped>
.toggle-song {
  color: #fff;
  border: none;
  border-radius: 12px;
  padding: 12px;
  margin: 12px;
  cursor: pointer;
  width: 5rem;
}

.hidden {
  display: none;
}

.iframe-target {
  margin-top: 4rem;
  width: 500px;
  border-radius: 12px;
}

.player {
  width: 500px;
  margin-top: -2rem;
}

.tape {
  background-color: #e8ebf3;
}

.holes {
  border: #000 4px solid;
  background-color: #5a697b;
  border-radius: 50px;
  position: relative;
  top: -70px;
  left: 85px;
  width: 11rem;
  height: 3rem;
  display: flex;
  justify-content: space-between;
}

.hole {
  background-color: #e8ebf3;
  border: #000 4px solid;
  border-radius: 50%;
  width: 2rem;
  height: 2rem;
  margin: 0.3rem;
}

.label {
  text-align: center;
  position: relative;
  top: -57px;
  font-size: 1rem;
  font-weight: bold;
}
</style>
