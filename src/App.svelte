<script>
   import Yawn from './lib/Yawn.svelte';

let yawns = [];
let images = [];
let gifs = [];

const occupiedSpaces = [];

function isOverlapping(newElement) {
  for (let existingElement of occupiedSpaces) {
    if (Math.abs(existingElement.x - newElement.x) < (existingElement.width + newElement.width) / 2 &&
        Math.abs(existingElement.y - newElement.y) < (existingElement.height + newElement.height) / 2) {
      return true;
    }
  }
  return false;
}

function getRandomPosition(width, height) {
  let position;
  do {
    position = {
      x: Math.random() * (window.innerWidth - 200),
      y: Math.random() * (window.innerHeight - 100),
      width,
      height
    };
  } while (isOverlapping(position));
  occupiedSpaces.push(position);
  return position;
}

  function addRandomYawns(count) {
    const sizes = ['small', 'medium', 'large'];
    const effects = ['static', 'fade', 'move'];

    for (let i = 0; i < count; i++) {
      const x = Math.random() * (window.innerWidth - 200);
      const y = Math.random() * (window.innerHeight - 100);
      const size = sizes[Math.floor(Math.random() * sizes.length)];
      const effect = effects[Math.floor(Math.random() * effects.length)];

      yawns.push({ x, y, size, effect });
    }
  }

  function addRandomImages(count) {
    const imageFiles = ['yawn1.webp', 'yawn2.webp', 'yawn3.webp', 'yawn4.webp', 'yawn5.webp', 'yawn6.webp'];

    for (let i = 0; i < count; i++) {
      const x = Math.random() * (window.innerWidth - 200);
      const y = Math.random() * (window.innerHeight - 100);
      const image = imageFiles[i];  // This ensures each image is used once

      images.push({ x, y, src: `../images/${image}` });
    }
  }

  function addRandomGifs(count) {
    const gifFiles = ['yawngif1.gif', 'yawngif2.gif', 'yawngif3.gif', 'yawngif4.gif'];
    const gifWidth = 250;
    const gifHeight = 250;  // Assume square GIFs for simplicity

    for (let i = 0; i < count && gifFiles.length > 0; i++) {
      const gifIndex = Math.floor(Math.random() * gifFiles.length);
      const gif = gifFiles.splice(gifIndex, 1)[0];
      const { x, y } = getRandomPosition(gifWidth, gifHeight);

      gifs.push({ x, y, src: `../images/${gif}` });
    }
  }

  addRandomYawns(60);
  addRandomImages(6);
  addRandomGifs(4);
</script>

<div id="container">
  {#each yawns as { x, y, size, effect }}
    <Yawn {x} {y} size={size} effect={effect} />
  {/each}
  {#each images as { x, y, src }}
    <img src={src} alt="" style="position: absolute; left: {x}px; top: {y}px; width: 150px; height: auto;" />
  {/each}
  {#each gifs as { x, y, src }}
    <img src={src} alt="" style="position: absolute; left: {x}px; top: {y}px; width: 150px; height: auto;" />
  {/each}
</div>

<style>
  /* Add styles if needed */
</style>