<script>
  import { createEventDispatcher } from "svelte";
  import { Icon, Input } from "sveltestrap";

  const dispatch = createEventDispatcher();

  export let bought;
  export let qty;
  export let name;
  export let price;
  export let total;
</script>

<tr>
  <td><Input type="checkbox" bind:checked={bought} /></td>
  <td><span>{qty}</span></td>
  <td><span>{name}</span></td>
  <td><span>{price}</span></td>
  <td><span>{total}</span></td>
  <td
    ><button class="trash" on:click={() => dispatch("deletePdt")}
      ><Icon name="trash-fill" /></button
    ></td
  >
</tr>

<style>
  .trash {
    padding: 0.2rem;
    border: none;
    background-color: white;
  }
</style>
