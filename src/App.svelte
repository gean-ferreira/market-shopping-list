<script>
  import ShoppingList from "./ShoppingList.svelte";
  import { Button, Table, Form, FormGroup, Label, Input } from "sveltestrap";

  let name,
    qty = 1,
    price;
  let totalPdt = 0,
    totalPurchases = 0;
  let list = JSON.parse(localStorage.getItem("shopping-list")) ?? [];

  $: {
    localStorage.setItem("shopping-list", JSON.stringify(list));
  }

  $: outstandingProducts = list.filter((pdt) => !pdt.bought).length;

  $: totalPurchases = list.reduce((amount, pdt) => {
    if (pdt.bought) {
      return amount + parseFloat(pdt.total);
    } else {
      return amount;
    }
  }, 0);

  function addPdt() {
    totalPdt = qty * price;

    list = [
      ...list,
      {
        bought: false,
        name: name,
        qty: qty,
        price: price.toFixed(2),
        total: totalPdt.toFixed(2),
      },
    ];

    name = "";
    qty = 1;
    price = "";
  }

  function deletePdt(item) {
    list = list.filter((i) => i !== item);
    totalPurchases -= item.total;
  }
</script>

<main on:submit|preventDefault={addPdt}>
  <h1>Shopping list</h1>

  <Form>
    <FormGroup>
      <Label>Name:</Label>
      <Input
        type="text"
        minlength="2"
        bind:value={name}
        placeholder="Product's name"
      />
    </FormGroup>
    <FormGroup>
      <Label>Quantity:</Label>
      <Input type="number" bind:value={qty} placeholder="1" min="1" />
    </FormGroup>
    <FormGroup>
      <Label>Price:</Label>
      <Input
        type="number"
        step="any"
        min="0.01"
        placeholder="US$0.99"
        bind:value={price}
      />
    </FormGroup>
    <Button color="primary" type="submit">Add</Button>
  </Form>

  {#if list.length === 0}
    <div class="emptyList">
      The list is empty. There are no products in the cart.
    </div>
  {:else}
    <Table class="tableList">
      <thead>
        <tr>
          <th />
          <th>Qty</th>
          <th>Name</th>
          <th>US$</th>
          <th>Total</th>
          <th />
        </tr>
        {#each list as item, i}
          <ShoppingList
            bind:bought={item.bought}
            bind:qty={item.qty}
            bind:name={item.name}
            bind:price={item.price}
            bind:total={item.total}
            on:deletePdt={() => deletePdt(item)}
          />
        {/each}
      </thead>
    </Table>
  {/if}

  <div>Outstanding products: {outstandingProducts}</div>
  <span>Total purchases:</span>
  <span>US$ {totalPurchases.toFixed(2)}</span>
</main>

<style>
  main {
    margin: 0 8px;
  }
  h1,
  .emptyList {
    text-align: center;
    margin: 16px 0;
  }
  th {
    padding: 2px;
  }
</style>
