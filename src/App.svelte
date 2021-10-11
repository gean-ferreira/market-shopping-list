<script>
  let totalPdt = 0;
  let totalPurchases = 0;

  let list = [];

  $: outstandingProducts = list.filter((item) => !item.bought).length;

  let name = null;
  let qty = null;
  let price = null;
  function addPdt() {
    totalPdt = qty.value * price.value;
    totalPurchases += totalPdt;

    list = [
      ...list,
      {
        bought: false,
        name: name.value,
        qty: qty.value,
        price: price.value,
        total: totalPdt,
      },
    ];

    name.value = "";
    qty.value = 1;
    price.value = "";
  }

  function deletePdt(item) {
    list = list.filter((i) => i !== item);
    totalPurchases -= item.total;
  }
</script>

<main>
  <h1>Shopping list</h1>

  <form on:submit|preventDefault={addPdt}>
    <input
      type="text"
      minlength="2"
      bind:this={name}
      placeholder="Product's name"
    />
    <input type="number" bind:this={qty} value="1" min="1" />
    <input
      type="number"
      step="any"
      min="0.01"
      placeholder="US$0.99"
      bind:this={price}
    />
    <button type="submit">Adicionar</button>
  </form>

  {#if list.length === 0}
    <div>The list is empty. There are no products in the cart.</div>
  {:else}
    <table class="tableList">
      <thead>
        <tr>
          <th />
          <th>Qty</th>
          <th>Name</th>
          <th>Price</th>
          <th>Total</th>
        </tr>
        {#each list as item, i}
          <tr>
            <td> <input type="checkbox" bind:checked={item.bought} /></td>
            <td> <span>{item.qty}</span></td>
            <td> <span>{item.name}</span></td>
            <td> <span>US$ {item.price}</span></td>
            <td> <span>US$ {item.total.toFixed(2)}</span></td>
            <td> <button on:click={deletePdt(item)}>Delete</button></td>
          </tr>
        {/each}
      </thead>
    </table>
  {/if}

  <div>Outstanding products: {outstandingProducts}</div>
  <div>Total purchases:</div>
  <span>US$ {totalPurchases.toFixed(2)}</span>
</main>

<style>
</style>
