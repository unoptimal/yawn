<script>
    export let x = 0;
    export let y = 0;
    export let size = 'medium'; // small, medium, large
    export let effect = 'static'; // static, fade, move
  </script>
  
  <div class={`yawn ${size} ${effect}`} style="left: {x}px; top: {y}px;">
    yawn
  </div>
  
  <style>
    .yawn {
      position: absolute;
      color: #555;
    }
    .small { font-size: 1em; }
    .medium { font-size: 2em; }
    .large { font-size: 4em; }
    .fade {
      animation: fadeInOut 5s infinite;
    }
    .move {
  animation: moveLeftRight 5s linear infinite;
}

  
    @keyframes fadeInOut {
      0%, 100% { opacity: 0; }
      50% { opacity: 1; }
    }
  
    @keyframes moveLeftRight {
    0%, 100% {
      transform: translateX(100%); /* Start and end off-screen to the right */
    }
    50% {
      transform: translateX(-100%); /* Move to off-screen to the left at the halfway point */
    }
  }

  .move {
    animation: moveLeftRight 10s linear infinite;
  }


  </style>
  