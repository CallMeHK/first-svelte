<script>
  let promise = getCard();
  let loading = true;
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
    loading = true;
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
    {#if loading}
      <p>Loading image...</p>
    {/if}
    <img
      src={card.image_uris.small}
      alt="card"
      style={loading && 'display:none'}
      on:load={() => {
        loading = false;
      }} />
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</div>
