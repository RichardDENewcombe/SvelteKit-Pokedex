<script context="module">
    export const load = async ({ page }) => ({
        props: {
            key: page.path,
        },
    })
</script>

<script>
    import Nav from '../components/nav.svelte'
    import PageTransition from '../components/pageTransition.svelte'
    export let key
</script>

<div class="container">
    <Nav />
    <PageTransition refresh={key}>
        <slot />
    </PageTransition>
</div>

<style>
    .container {
        padding: 1rem;
        max-width: 110rem;
        margin-left: auto;
        margin-right: auto;
    }

</style>