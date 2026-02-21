<script lang="ts">
  import "./styles.css";
  import { onMount } from "svelte";

  export let emit: (key: string, value: any) => void;
  export let settings: {
    autoStart: boolean;
    emitStartTime: boolean;
    emitOnPause: boolean;
    displayFormat: "hms" | "ms";
    tickInterval: number;
  };

  let seconds = 0;
  let running = false;
  let paused = false;
  let interval: number | null = null;

  function start() {
    if (!running && settings.emitStartTime) {
      emit("startTime", new Date().toISOString());
    }
    running = true;
    paused = false;
    tick();
  }

  function pause() {
    paused = !paused;

    if (paused && interval) {
      clearInterval(interval);
      interval = null;

      if (settings.emitOnPause) {
        emit("elapsedMinutes", Math.floor(seconds / 60));
      }
    } else if (!paused) {
      tick();
    }
  }

  function stop() {
    running = false;
    paused = false;
    if (interval) clearInterval(interval);

    emit("elapsedSeconds", seconds);
    emit("elapsedMinutes", Math.floor(seconds / 60));

    seconds = 0;
    interval = null;
  }

  function tick() {
    if (interval) return;
    interval = setInterval(() => {
      seconds += settings.tickInterval;
    }, settings.tickInterval * 1000);
  }

  function format(s: number) {
    if (settings.displayFormat === "ms") {
      const m = Math.floor(s / 60);
      const sec = s % 60;
      return `${String(m).padStart(2, "0")}:${String(sec).padStart(2, "0")}`;
    }
    return new Date(s * 1000).toISOString().substring(11, 19);
  }

  onMount(() => {
    if (settings.autoStart) {
      start();
    }
  });
</script>

<div class="stopwatch">
  <div class="time">{format(seconds)}</div>

  <button on:click={start} disabled={running && !paused}>
    Start
  </button>

  <button
    on:click={pause}
    class:pause={paused}
    disabled={!running}
  >
    Pause
  </button>

  <button on:click={stop} disabled={!running}>
    Stop
  </button>
</div>
