<svelte:options tag="mail-me" />

<script lang="ts">
  import { onMount } from "svelte";

  let baseURL =
    "https://mail3-app-git-feat-mail-me-button-mail3-postoffice.vercel.app";
  export let variant = "solid";
  export let lite = false;
  export let address: string;
  let count = -1;
  $: displayCount = count > 99 ? "99+" : count;
  $: text = count < 0 ? "Mail me" : "Check Mail";

  let src: string = `${baseURL}/api/logo`;

  onMount(() => {
    const eventListener = (event: MessageEvent) => {
      if (event.origin === baseURL) {
        count = event.data.total;
      }
    };
    window.addEventListener("message", eventListener);

    return () => {
      window.removeEventListener("message", eventListener);
    };
  });
</script>

<a
  href={count < 0 ? `${baseURL}/message/edit?to=${address}` : baseURL}
  target="_blank"
  class="container"
  class:solid={variant === "solid"}
  class:outline={variant === "outline"}
  class:ghost={variant === "ghost"}
  class:lite
  {...$$restProps}
>
  <div class="content">
    <div class="img">
      <img {src} alt={text} />
      {#if count >= 0}
        <span class="badge" class:big-count={displayCount !== count}
          >{displayCount}</span
        >
      {/if}
    </div>
    {#if !lite}
      <span>{text}</span>
    {/if}
  </div>
</a>
{#if count === -1}
  <iframe
    title="Mail3"
    src={`${baseURL}/unread${address ? `?from=${address}` : ""}`}
    style="display: none;"
  />
{/if}

<style>
  .container {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    text-decoration: none;
    border-radius: 8px;
    font-size: 12px;
    padding: 12px 0;
    width: 124px;
    font-family: "Poppins", -apple-system, BlinkMacSystemFont, Helvetica Neue,
      sans-serif;
  }
  .content {
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  .img {
    position: relative;
  }
  .badge {
    position: absolute;
    top: -8px;
    right: -6px;
    width: 18px;
    height: 18px;
    background: #ff0c00;
    border-radius: 50%;
    display: flex;
    align-items: center;
    color: white;
    justify-content: center;
  }
  .badge.big-count {
    width: 30px;
    border-radius: 26px;
    right: -20px;
  }
  .content img {
    width: 16px;
    height: 16px;
    margin-right: 4px;
  }

  .solid {
    background: black;
    color: white;
  }
  .outline {
    border: 1px solid #4e51f4;
    color: black;
  }
  .ghost {
    border: none;
    background: transparent;
  }
  .lite {
    border-radius: 40px;
    width: 36px;
    height: 36px;
    padding: 0;
  }
</style>
