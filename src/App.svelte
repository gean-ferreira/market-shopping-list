<script>
  let totalPdt = 0;
  let totalPurchases = 0;

  let list = [];

  function addPdt() {
    const name = document.getElementById("namePdt").value;
    const qty = document.getElementById("qtyPdt").value;
    const price = document.getElementById("pricePdt").value;

    totalPdt = qty * price;
    totalPurchases += totalPdt;

    list = [
      ...list,
      {
        name: name,
        qty: qty,
        price: price,
        total: totalPdt,
      },
    ];
  }

  function deletePdt(item) {
    list = list.filter((i) => i !== item);
  }
</script>

<main>
  <h1>Shopping list</h1>
  <input type="text" name="" id="namePdt" placeholder="Product's name" />
  <input type="number" name="" id="qtyPdt" value="1" />
  <span>US$</span>
  <input type="number" name="" id="pricePdt" value="0.99" />
  <button on:click={addPdt}>Adicionar</button>

  {#if list.length === 0}
    <div>The list is empty. There are no products in the cart.</div>
  {:else}
    <ul class="shopping-list">
      {#each list as item, i}
        <li>
          <input type="checkbox" />
          <span>{item.qty}</span>
          <span>{item.name}</span>
          <span>US$ {item.price}</span>
          <span>US$ {item.total}</span>
          <button on:click={deletePdt(item)}>Delete</button>
        </li>
      {/each}
      <div>Total purchases:</div>
      <span>US$ {totalPurchases.toFixed(2)}</span>
    </ul>
  {/if}
</main>

<style>
  .shopping-list {
    padding: 0px;
    list-style-type: none;
  }
</style>
