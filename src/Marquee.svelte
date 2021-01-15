<script>
  import { onMount } from "svelte";
  export let text;
  let style = "";
  const resize = () => {
    const duration = Math.trunc(window.innerWidth / 60) + text.length / 10;
    const textWidth = text.length * 16;
    style = `animation-duration:${duration}s;` + `width:${textWidth}px;`;
  };

  onMount(() => {
    resize();
  });
</script>

<style>
  .marquee {
    width: 100%;
    overflow: hidden;
  }

  .marquee_text {
    padding-left: 100%;
    text-align: left;
    white-space: nowrap;

    animation-name: marquee;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
  }

  @keyframes marquee {
    from {
      transform: translate(0%);
    }
    100%,
    to {
      transform: translate(-100%);
    }
  }
</style>

<svelte:window on:resize={resize} />
<div class="marquee">
  <div class="marquee_text" {style}>{text}</div>
</div>
