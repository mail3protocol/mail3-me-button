<svelte:options tag="mail3-me" />

<script lang="ts">
  import { onMount } from "svelte";
  const emailReg = /^\S+@\S+\.\S+$/;
  let baseURL = "https://app.mail3.me";
  export let variant = "solid";
  export let lite = false;
  export let to: string = "";
  export let icon_type: string = "solid";
  export let icon_style: string = "";
  export let css: string = '';
  if (to && !emailReg.test(to)) {
    console.error(
      "Please pass a valid email address, current address: " + to
    );
  }
  let count = -1;
  $: displayCount = count > 99 ? "99+" : count;
  $: text = count <= 0 ? "Mail³ me" : "Open inbox";
  $: src = `${baseURL}/icons/${icon_type}.png`;
  // https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#boolean-attributes
  $: isLite = lite !== false;
  let hostname = location.hostname;
  const buildUTMQuery = (ev: string) =>
    `utm_source=${hostname}&utm_medium=${ev}`;

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
  href={count <= 0
    ? `${baseURL}/message/edit?${buildUTMQuery("click_mail_me_button")}${
        to ? `&to=${to}` : ""
      }`
    : `${baseURL}/?${buildUTMQuery("click_check_mail_button")}`}
  target="_blank"
  class="container"
  class:solid={variant === "solid"}
  class:outline={variant === "outline"}
  class:ghost={variant === "ghost"}
  class:lite={isLite}
  style={css ? css : $$restProps.style}
  {...$$restProps}
>
  <div class="content">
    <div class="img">
      <img {src} style={icon_style} class:circle={isLite} alt={text} />
      {#if count > 0}
        <span class="badge" class:big-count={displayCount !== count}
          >{displayCount}</span
        >
      {/if}
    </div>
    {#if !isLite}
      <span>{text}</span>
    {/if}
  </div>
</a>
{#if count === -1}
  <iframe
    title="Mail3"
    src={`${baseURL}/unread?${buildUTMQuery(
      "visit_mail_me_check_mail_button"
    )}${to ? `&from=${to}` : ""}`}
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
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .badge {
    position: absolute;
    top: -8px;
    right: -6px;
    width: 14px;
    font-size: 12px;
    height: 14px;
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
  .content .circle {
    margin-right: 0;
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
    padding: 0;
  }
  .lite {
    border-radius: 40px;
    width: 36px;
    height: 36px;
    padding: 0;
  }
</style>
