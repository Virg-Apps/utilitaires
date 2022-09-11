<script lang="ts">
    import Menu from "$lib/components/layout/menu.svelte";
    import Header from "$lib/components/layout/header.svelte";
</script>

<div id="wrapper">
    <Menu/>

    <Header/>

    <main>
        <slot></slot>
    </main>
</div>

<style>
    #wrapper {
        display: grid;
        grid-template-areas:
            'menu header'
            'menu main';
        grid-template-columns: 250px 1fr;
        grid-template-rows: 50px 1fr;
    }

    main {
        grid-area: main
    }
</style>