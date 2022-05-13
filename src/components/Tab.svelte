<script>
    import { getContext, onMount } from "svelte";
    import { ui } from "@clientio/rappid";
    import { TABS } from "./Tabs.svelte";

    const tab = {};
    const { registerTab, selectTab, removeTab, selectedTab } = getContext(TABS);

    registerTab(tab);

    /* 
        Props - Svelte convention is to use 'export let' for props
    */
    export let title;

    onMount(async () => {
        const app = document.querySelector(".app");

        new ui.Tooltip({
            theme: "material",
            rootTarget: app,
            container: app,
            target: "[data-tooltip]",
            direction: ui.Tooltip.TooltipArrowPosition.Auto,
            position: ui.Tooltip.TooltipPosition.Top,
            padding: 10,
            animation: true,
        });
    });
</script>

<button
    class="btn"
    class:selected={$selectedTab === tab}
    on:click={() => selectTab(tab)}
>
    <slot />
    <button
        class="btn-remove"
        on:click={() => removeTab(tab)}
        data-tooltip={`Remove ${title} tab`}
        data-tooltip-position="top">x</button
    >
</button>

<style>
    .btn {
        background: none;
        display: inline-block;
        border: 1px solid transparent;
        border-bottom: none;
        bottom: -1px;
        position: relative;
        list-style: none;
        padding: 6px 12px;
        cursor: pointer;
    }

    .selected {
        background: #fff;
        border-color: #aaa;
        color: black;
        border-radius: 5px 5px 0 0;
    }
</style>
