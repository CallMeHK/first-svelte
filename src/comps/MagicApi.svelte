<script>
  let promise = getCard();

  async function getCard() {
    const res = await fetch(`https://api.scryfall.com/cards/random`);
    const card = await res.json();

    if (res.ok) {
      return card;
    } else {
      throw new Error(card);
    }
  }

  function onClick() {
    promise = getCard();
  }
</script>

<div>
  {#await promise}
    <p>...waiting</p>
  {:then card}
    <p>{card.name}</p>
    <div>
      <button on:click={onClick}>Fetch again</button>
    </div>
    <img src={card.image_uris.small} alt="card" />
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</div>
