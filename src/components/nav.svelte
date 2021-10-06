<script lang="ts">
    import { page } from '$app/stores'
</script>

{#if $page.path != "/"}
    <nav class="nav">
        <a class="link" href="/">Home</a>
    </nav>
{/if}

<style>
    .nav {
        display: flex;
        justify-content: center;
        width: 100%;
    }

    .link {
        margin-left: 1rem;
        margin-right: 1rem;
        font-size: 1.125rem;
        line-height: 1.75rem;
    }

    a {
        text-decoration: none;
        color: black;
    }

    a:visited {
        text-decoration: none;
        color: black;
    }
</style>