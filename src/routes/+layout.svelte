<script lang="ts">
    import Menu from "$lib/components/layout/menu.svelte";
    import Header from "$lib/components/layout/header.svelte";

    export const prerender = true;
</script>

<Menu/>

<Header/>

<main>
    <slot></slot>
</main>