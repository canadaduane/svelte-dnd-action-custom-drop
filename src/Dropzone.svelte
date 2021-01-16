<script>
  import { createEventDispatcher } from "svelte";
  import { writable } from "svelte/store";

  import { dropzones } from "./dropzones";
  import { uuidv4 } from "./uuid";

  export let list;
  export let selected;

  let dropzoneId = uuidv4();
  const BLINK_DURATION = 290;
  const dispatch = createEventDispatcher();

  const active = writable(false);

  active.subscribe(($active) => {
    if ($active) {
      setTimeout(() => active.set(false), BLINK_DURATION);
    }
  });

  $: dropzones.set(dropzoneId, { list, dispatch, active });

  let items = [];
</script>

<button
  data-dropzone-id={dropzoneId}
  class="dropzone-{list.category}"
  class:selected
  class:blink={$active}
  on:click>
  <slot {list}>{list.name}</slot>
</button>

<style>
  button {
    all: unset;
    display: block;

    border-width: 1px;
    border-style: solid;
    border-radius: 5px;

    width: 68px;
    height: 40px;

    margin: 8px;
    padding: 2px;

    text-align: center;
    overflow: hidden;

    cursor: pointer;
  }
  button:hover {
    background-color: rgb(243, 179, 179);
  }
  .selected {
    border: 1px solid red !important;
    box-shadow: 0px 0px 0px 2px red;
  }

  @keyframes border-blink {
    from,
    to {
      box-shadow: inset 0px 0px 0px 2px transparent;
    }
    50% {
      box-shadow: inset 0px 0px 0px 2px black;
    }
  }
  .blink {
    animation: border-blink 0.15s step-end infinite;
  }

  :global(button.dropzone-favorite, button.dropzone-relm) {
    border-color: orange;
  }
  :global(button.dropzone-trash) {
    border-color: transparent;
    background-color: transparent !important;
  }
</style>
