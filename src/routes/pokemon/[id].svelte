<script lang="ts" context="module">

    export async function load({page}) {
        const id: number = page.params.id;
        let res = await fetch(`https://pokeapi.co/api/v2/pokemon/${id}`);
        const pokemon = await res.json()

        let previousId: number;
        let previousPokemon;
        if (id == 1) {
            previousId = null;
        } else {
            previousId = Number(page.params.id) - 1;
        }
        if( previousId ) {
            res = await fetch(`https://pokeapi.co/api/v2/pokemon/${previousId}`);
            previousPokemon = await res.json()
        } else {
            previousPokemon = null
        }

        let nextId: number;
        let nextPokemon;
        if (id == 251) {
            nextId = null;
        } else {
            nextId = Number(page.params.id) + 1;
        }
        if ( nextId ) {
            res = await fetch(`https://pokeapi.co/api/v2/pokemon/${nextId}`);
            nextPokemon = await res.json()
        } else {
            nextPokemon = null
        }

        return {props: {
            pokemon,
            nextPokemon,
            previousPokemon
        }}
    }

</script>

<script lang="ts">

    export let pokemon;
    export let nextPokemon;
    export let previousPokemon;

    function properCase(phrase: string): string {
        return phrase.split(' ').map(w => w[0].toUpperCase() + w.substr(1).toLowerCase()).join(' ')
    }

    function checkTypes(pokemonObject): string {
        if (pokemonObject.types[1]) {
            return properCase(pokemonObject.types[0].type.name) + " " + properCase(pokemonObject.types[1].type.name)
        }
        return properCase(pokemonObject.types[0].type.name)
    }

    const type: string = checkTypes(pokemon)

</script>

<div>
    <div class="pokemonBar">
        {#if previousPokemon}
            <a href={`/pokemon/${previousPokemon.id}`} >
                <img src={previousPokemon.sprites['front_default']} alt={previousPokemon.name}>
                <h4>{String(previousPokemon.id).padStart(3, "0")} - {previousPokemon.name}</h4>
            </a>
        {:else}
            <div class="paddingBox"></div>
        {/if}

        <h1>{pokemon.name}</h1>

        {#if nextPokemon}
            <a href={`/pokemon/${nextPokemon.id}`} >
                <img src={nextPokemon.sprites['front_default']} alt={nextPokemon.name}>
                <h4>{String(nextPokemon.id).padStart(3, "0")} - {nextPokemon.name}</h4>
            </a>
        {:else}
            <div class="paddingBox"></div>
        {/if}
    </div>

    <img src={pokemon.sprites['front_default']} alt={pokemon.name}>

    <p>Type: <strong>{type}</strong> | Height: <strong>{pokemon.height * 10} cm</strong> | Weight: <strong>{pokemon.weight / 10} kg</strong></p> 

</div>


<style>

    .paddingBox {
        height: 10rem;
        width: 10rem;
        padding-left: 20rem;
        padding-right: 20rem;
    }

    a {
        padding-left: 20rem;
        padding-right: 20rem;
        text-decoration: none;
    }

    img {
        height: 10rem;
        width: 10rem;
        }

    h1 {
        font-size: 2.25rem;
        line-height: 2.5rem;
        text-align: center;
        margin-top: 2rem;
        margin-bottom: .5rem;
        text-transform: capitalize;
    }

    div {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .pokemonBar {
        flex-direction: row;
    }

    h4 {
        text-transform: capitalize;
        text-align: center;
    }

    a, a:visited, a:hover, a:active {
        color: inherit;
}

</style>