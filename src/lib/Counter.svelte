<style>
  .swipe-holder {
    height: 100%;
    width: 100%;
  }
  
  video {
    height: 100%;
    /* width: 25vw; */
  }

  @media (max-width: 768px) { /* Adjust the breakpoint as needed */
    video {
      max-width: 100%;
    }
  }
</style>

<script>
  import { Swipe, SwipeItem } from 'svelte-swipe'
  import IMG1 from './assets/reels/v1.mp4'
  import IMG2 from './assets/reels/v2.mp4'
  import IMG3 from './assets/reels/v3.mp4'
  import { onMount } from 'svelte'

  const swipeConfig = {
    autoplay: false,
    delay: 2000,
    showIndicators: true,
    transitionDuration: 1000,
    defaultIndex: 0
  }

  let activeVideo = null;
  onMount(() => {
    activeVideo = document.getElementById('active_1').querySelector('video');
    activeVideo.play();
  });
  function handleSlideChange(index) {
    // Pause the previously active video
    if (activeVideo) {
      activeVideo.pause();
      activeVideo.currentTime = 0;
    }

    // Get the video element of the current slide
    const currentSlide = document.getElementById(`active_${index + 1}`);
    activeVideo = currentSlide.querySelector('video');

    // Play the video
    activeVideo.play();
  }
</script>

<div class="swipe-holder">
  <Swipe {...swipeConfig} is_vertical="{true}" on:slidechange="{handleSlideChange}">
    <SwipeItem>
      <video autoplay="true" id="active_1" class="detail" loop>
        <source src="{IMG1}" type="video/mp4" />
        Your browser does not support the video tag.
      </video>
    </SwipeItem>

    <SwipeItem>
      <video autoplay="true" id="active_2" class="detail" loop>
        <source src="{IMG2}" type="video/mp4" />
        Your browser does not support the video tag.
      </video>
    </SwipeItem>

    <SwipeItem>
      <video autoplay="true" id="active_3" class="detail" loop>
        <source src="{IMG3}" type="video/mp4" />
        Your browser does not support the video tag.
      </video>
    </SwipeItem>
  </Swipe>
</div>
