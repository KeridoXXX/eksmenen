<script setup>
import { reactive, onMounted, nextTick } from "vue";
import { Draggable, Droppable } from "@shopify/draggable";
import Helements from "./components/Helements.vue";

const logoUrl = "http://localhost:8080/logos/";

let draggable;

const state = reactive({
  bands: null,
});

async function getBands() {
  const response = await fetch("http://localhost:8080/bands");
  state.bands = await response.json();
  console.log("data fetched");

  await nextTick();
  // initDraggable();
  initDroppable();
}

// function initDraggable() {
//   console.log("init draggable");
//   draggable = new Draggable(document.querySelectorAll(".tape"), {
//     draggable: ".tape",
//   });

//   draggable.on("drag:start", () => console.log("drag:start"));
//   draggable.on("drag:move", () => console.log("drag:move"));
//   draggable.on("drag:stop", () => console.log("drag:stop"));
// }

let droppableInitialized = false;

function initDroppable() {
  if (droppableInitialized) {
    return;
  }

  console.log("init droppable");
  const dropzones = document.querySelectorAll(".dropzone");

  dropzones.forEach((dropzone) => {
    const droppable = new Droppable(dropzone, {
      draggable: ".tape",
      dropzone: ".dropzone",
    });

    droppable.on("droppable:start", () => console.log("droppable:start"));
    droppable.on("droppable:dropped", () => console.log("droppable:dropped"));
    droppable.on("droppable:returned", () => console.log("droppable:returned"));
    droppable.on("droppable:stop", () => console.log("droppable:stop"));
  });

  droppableInitialized = true;
}

getBands();
</script>

<template>
  <header><Helements></Helements></header>
  <main>
    <div class="grid grid-cols-2">
      <div class="dropzone grid gap-2 overflow-scroll h-screen justify-center">
        <div
          class="tape bg-slate-400 p-4 w-60 flex flex-row justify-between items-center"
          v-for="band in state.bands"
        >
          <div>
            <p>{{ band.name }}</p>
            <p>{{ band.genre }}</p>
          </div>
          <img
            class="h-8 w-8"
            :src="
              band.logo.startsWith('https://') ? band.logo : logoUrl + band.logo
            "
            alt=""
          />
        </div>
      </div>
      <div class="dropzone bg-red-200 border-dotted border-black border-2">
        <p>DROPZONE</p>
      </div>
    </div>
  </main>
  <footer></footer>
</template>

<style scoped></style>
