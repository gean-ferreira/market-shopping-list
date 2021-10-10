<script>
  import { each, space } from "svelte/internal";

  let list = [
    { name: "Apple", qty: 2, price: 2.99 },
    { name: "Banana", qty: 5, price: 1.99 },
    { name: "Orange", qty: 3, price: 0.69 },
    { name: "Tea", qty: 1, price: 4.99 },
  ];
</script>

<main>
  <h1>Shopping list</h1>
  <input type="text" name="" id="" placeholder="Product's name" />
  <input type="number" name="" id="" value="1" />
  <span>US$</span>
  <input type="number" name="" id="" value="0.99" />
  <button>Adicionar</button>
  <ul class="shopping-list">
    {#each list as item, i}
      <li>
        <input type="checkbox" />
        <span>{item.qty}</span>
        <span>{item.name}</span>
        <span>{item.price}</span>
        <button>Delete</button>
      </li>
    {/each}
  </ul>
</main>

<style>
  .shopping-list {
    padding: 0px;
    list-style-type: none;
  }
</style>
