<script lang="ts">
  export let dialogElement: HTMLDialogElement;
  export let title: string;
  export let titleColor = "text-primary";
  export let modalOnClose: () => void = () => {
    /* Don't do anything on close by default */
  };

  $: if (/success/i.test(title)) {
    titleColor = "text-primary";
  } else if (/error/i.test(title) || /delete/i.test(title)) {
    titleColor = "text-error";
  } else if (/warning/i.test(title)) {
    titleColor = "text-warning";
  }
</script>

<dialog
  bind:this={dialogElement}
  id={title}
  class="modal modal-bottom sm:modal-middle"
  on:close={modalOnClose}
>
  <form class="modal-box text-white" method="dialog">
    <button class="btn btn-sm btn-circle absolute right-2 top-2 bg-black outline-none" data-testid="close-modal-button">
      ✕
    </button>
    <h2 class="font-bold text-lg {titleColor} mb-5">{title}</h2>
    <slot />
  </form>
  <form class="modal-backdrop bg-black bg-opacity-50" method="dialog">
    <button>close</button>
  </form>
</dialog>
