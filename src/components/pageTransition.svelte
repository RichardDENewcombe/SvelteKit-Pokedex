<script lang="ts">
    import { fade } from "svelte/transition"
    export let refresh: string = ""
</script>

{#key refresh}
    <div in:fade={{ duration: 100, delay: 100 }} out:fade={{ duration: 50 }}>
        <slot />
    </div>
{/key}