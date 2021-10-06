<script lang="ts">

    import { pokemon } from "../stores/pokestore"
    import PokemonCard from '../components/pokemonCard.svelte'

    let searchTerm: string = "";
    let filteredPokemon: any[] = [];

    $: {
        if (searchTerm) {
            filteredPokemon = $pokemon.filter(pokemon => pokemon.name.toLowerCase().includes(searchTerm.toLowerCase()))
        } else {
            filteredPokemon = [... $pokemon]
        }
    }

</script>

<svelte:head>
    <title>
        Pokedex
    </title>
</svelte:head>

<div class="container">
    <input bind:value={searchTerm} type="text" placeholder="Search">
</div>
<div class="pokedex">
    {#each filteredPokemon as pokemon}
        <PokemonCard {pokemon} />
    {/each}
</div>

<style>

    input {
        width: 25%;
        border-radius: 1rem;
        font-size: 1.125rem;
        line-height: 1.75rem;
        padding: 1rem;
        margin-top: 1rem;
        border-width: 2px;
        border-color: rgba(229, 231, 235, 1);
    }

    .container {
        display: flex;
        justify-content: center;
    }

    .pokedex {
        display: flex;
        padding-top: 1rem;
        padding-bottom: 1rem;
        justify-items: center;
        flex-wrap: wrap;
        gap: 1rem;
        margin: 1rem;
        justify-content: center;
    }

</style>