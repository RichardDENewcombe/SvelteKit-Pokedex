<script lang="ts">

    interface Pokemon {
        name: string;
        id: number;
        image: any;
    }

    export let pokemon: Pokemon

</script>

<a href={`/pokemon/${pokemon.id}`} >
    <img src={pokemon.image} alt={pokemon.name}>
    <h2>{pokemon.name}</h2>
</a>


<style>

    a {
        list-style-type: none;
        padding: 1rem;
        background-image: url("../images/pokeball.svg");
        background-size: contain;
        background-repeat: no-repeat;
        color: rgba(31, 41, 55, 1);
        border-radius: 0.5rem;
        display: flex;
        flex-direction: column;
        text-decoration: none;
    }

    img {
        height: 10rem;
        width: 10rem;
    }
    h2 {
        text-transform: capitalize;
        text-align: center;
    }

</style>