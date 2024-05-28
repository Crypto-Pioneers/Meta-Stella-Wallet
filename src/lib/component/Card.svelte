<script>
  import { onMount } from "svelte";
  import { writable } from "svelte/store";

  export let theme = "default";
  export let stopRecording = false;

  let mouseData = writable([]);
  let recording = true;
  let oldData = {
    point: {
      x: 0,
      y: 0,
    },
    timestamp: getCurrentTimeStamp(),
  };

  function getCurrentTimeStamp() {
    const dNow = new Date();
    return dNow.valueOf(); // 1673445066359
  }

  function getDistance(oldData, newData) {
    return Math.sqrt(
      Math.pow(Math.abs(oldData.point.x - newData.point.x), 2) +
        Math.pow(Math.abs(oldData.point.y - newData.point.y), 2)
    );
  }

  function getTimeInterval(oldData, newData) {
    return newData.timestamp - oldData.timestamp;
  }

  function recordMouseMovement(
    oldData,
    event,
    distanceThreshold,
    timeThreshold,
    recordingFlag
  ) {
    if (recordingFlag) {
      const newData = {
        point: {
          x: event.clientX,
          y: event.clientY,
        },
        timestamp: getCurrentTimeStamp(),
      };

      const distance = getDistance(oldData, newData);
      const timeInterval = getTimeInterval(oldData, newData);
      console.log("distance-time interval", distance, timeInterval);
      if (distance >= distanceThreshold && timeInterval > timeThreshold) {
        mouseData.update((data) => [
          ...data,
          {
            point: newData.point,
            timestamp: timeInterval,
          },
        ]);

        mouseData.subscribe((value) => {
          console.log(value);
        });

        return newData;
      }
    }
    return oldData;
  }

  function handleMouseMove(event) {
    const temp = recordMouseMovement(oldData, event, 10, 10000, true);
    oldData = { point: temp.point, timestamp: temp.timestamp };
  }

  onMount(() => {
    window.addEventListener("mousemove", handleMouseMove);
    return () => {
      window.removeEventListener("mousemove", handleMouseMove);
    };
  });

  $: if (stopRecording) {
    recording = false;
  }
</script>

<div class="card {theme}">
  <div class="content">
    <slot name="content">Card Content</slot>
    <div class="mouse-data">
      <!-- {$mouseData.map(point => (
        <div>
          X: {point.x}, Y: {point.y}, Time: {new Date(point.time).toLocaleTimeString()}
        </div>
      ))} -->
    </div>
  </div>
</div>

<style>
  .card {
    perspective: 1000px;
    width: 300px;
    height: 200px;
    margin: 20px;
    transition: transform 0.3s ease;
  }

  .card:hover {
    transform: rotateY(20deg) rotateX(10deg);
  }

  .content {
    background: var(--background, #fff);
    border-radius: 15px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    padding: 20px;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    transition:
      background 0.3s ease,
      box-shadow 0.3s ease;
  }

  .default {
    --background: #f0f0f0;
    --shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }

  .theme-dark {
    --background: #333;
    --shadow: 0 10px 20px rgba(0, 0, 0, 0.5);
    color: #fff;
  }

  .mouse-data {
    margin-top: 10px;
    font-size: 12px;
    max-height: 100px;
    overflow-y: auto;
  }
</style>
