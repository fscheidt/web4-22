<script>
let promise = getMovies();
async function getMovies() {
    const res = await fetch(
        `http://localhost:8000/movies`
    );
    const text = await res.json();
    if (res.ok) {
        return text;
    } else {throw new Error(text); }
}
function handleClick() {
    promise = getMovies();
}
</script>
<button on:click={handleClick}>
list movies
</button>

{#await promise}
    <p>...waiting</p>
{:then movies}
    {#each movies as m }
        <p>{m.id}</p>
        <p>{m.title}</p>
        <p>{m.genre}</p>
    {/each}
{:catch error}
    <p style="color: red">{error.message}</p>
{/await}
