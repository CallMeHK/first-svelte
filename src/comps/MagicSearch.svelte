<script>
  let search = "";
  let loading = false;
  let timeout = null
  let results = {};

  function getCards() {
    console.log(search)
    if(!!timeout){
      clearTimeout(timeout)
    }
    if (search !== "") {
      loading = true;
      timeout = setTimeout(cardQuery, 1500);
    }
  }

  function cardQuery() {
    const query = encodeURIComponent(search.trim())
    console.log(`Fetching ${query}`)
    return fetch(
      `https://api.scryfall.com/cards/named?fuzzy=${query}`
    )
      .then(res => res.json())
      .then(res => {
        console.log(res)
        results = res;
        loading = false;
      });
  }
</script>

<div>
  <h2>Magic Search</h2>
  <div>
    <input
      bind:value={search}
      placeholder="Enter a card name"
      on:input={getCards} />
    {#if !loading && search !== ''}
      <div> {JSON.stringify(results)} </div>
    {/if}
  </div>
</div>
