<script>
    import { getContext } from "svelte";
    import { TABS } from "./Tabs.svelte";

    const { addTab } = getContext(TABS);
</script>

<div class="tabs-list">
    <slot />
    <button
        on:click={() => addTab()}
        data-tooltip="Add a new tab"
        data-tooltip-position="top">+</button
    >
</div>

<style>
</style>
