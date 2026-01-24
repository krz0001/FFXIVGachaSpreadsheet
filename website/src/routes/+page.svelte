<script lang="ts">
    import {getLastUpdate} from "$lib/utils";
    import CardLink from "../component/CardLink.svelte";
    import { browser } from '$app/environment';
</script>

<svelte:head>
    <title>Home</title>

    <meta property="og:site_name" content="Home">
    <meta property="og:title" content="Home">
    <meta name="description" content="A collection of probabilities." />
    <meta property="og:description" content="A collection of probabilities." />
</svelte:head>

<div class="col-12">
    <section class="hero">
        <div class="hero-body">
            <p class="title">Final Fantasy 14 %-Stats</p>
            {#await getLastUpdate(browser)}
                <p class="subtitle has-skeleton">
                Last Update:
                </p>
            {:then value}
                <p class="subtitle">
                    Last Update: {value}
                </p>
            {/await}
        </div>
    </section>

    <!-- <div class="row row-cols-1 row-cols-md-3 g-4 mb-3"> -->
    <div class="columns is-multiline">
        <CardLink cardTitle={'Random Coffers'} cardIcon={'061000/061812'} cardLink={'coffer/'} />
        <CardLink cardTitle={'Lockboxes'} cardIcon={'061000/061808'} cardLink={'lockbox/'} />
        <CardLink cardTitle={'Card Packs'} cardIcon={'061000/061820'} cardLink={'card/'} />
        <CardLink cardTitle={'Ventures'} cardIcon={'061000/061818'} cardLink={'venture/'} />
        <CardLink cardTitle={'Eureka Bunnies'} cardIcon={'061000/061833'} cardLink={'bunny/'} />
        <CardLink cardTitle={'Deep Dungeons'} cardIcon={'061000/061824'} cardLink={'deep/'} />
        <CardLink cardTitle={'Desynthesis'} cardIcon={'000000/000120'} cardLink={'desynth/'} />
        <CardLink cardTitle={'Loot'} cardIcon={'061000/061801'} cardLink={'loot/'} />
        <CardLink cardTitle={'Occult'} cardIcon={'061000/061851'} cardLink={'occult/'} />
        <CardLink cardTitle={'Submarine Loot'} cardIcon={'063000/063191'} cardLink={'submarine/'} />
        <CardLink cardTitle={'Logograms and Fragments'} cardIcon={'061000/061837'} cardLink={'logofrag/'} />
    </div>
</div>