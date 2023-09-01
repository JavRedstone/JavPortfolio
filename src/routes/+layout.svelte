<style>
    :global(body),
    :global(html)
    :global(main) {
        display: block !important;
        height: auto !important;
        width: auto !important;
        position: static !important;
        margin: 0 !important;
        padding: 0 !important;

        font-family: 'Poppins', sans-serif !important;
    }

    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        width: 100vw;
        overflow: hidden;
    }
</style>
<!-- <svelte:head>
    {#if darkMode}
        <link rel="stylesheet" href='../theme/dark/smui-dark.css' media="print" />
        <link rel="stylesheet" href='../theme/smui.css' media="screen" />
    {:else}
        <link rel="stylesheet" href='../theme/dark/smui-dark.css' />
    {/if}
</svelte:head> -->
<main>
    <TopAppBar bind:this={topAppBar} variant="standard" dense>
        <Row>
            <Section align="start" toolbar>
                <Title>Welcome to JavPortfolio.</Title>
            </Section>
            <!-- <Section align="end" toolbar>
                <IconButton class="material-symbols-outlined" on:click={switchDarkLight}>
                    {#if darkMode}
                        dark_mode
                    {:else}
                        light_mode
                    {/if}
                </IconButton>
            </Section> -->
        </Row>
    </TopAppBar>
    <div style="margin-top: 48px; padding: 48px">
        <slot />
    </div>
</main>
<script lang="ts">
    import { onMount } from 'svelte';
    import TopAppBar, { Row, Section, Title } from '@smui/top-app-bar';
    // import IconButton from '@smui/icon-button';

    import '../theme/dark/smui-dark.css';
    // import '../theme/smui.css';
    
    let topAppBar: TopAppBar;
    let darkMode: boolean = false;

    onMount(() => {
        darkMode = window.matchMedia('(prefers-color-scheme: dark)').matches;
    });

	function switchDarkLight() {
        darkMode = !darkMode;
	}
</script>