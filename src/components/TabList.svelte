<script>
    import { getContext, onMount } from 'svelte';
    import { ui } from '@clientio/rappid';
	import { TABS } from './Tabs.svelte';

    const { addTab } = getContext(TABS);

    onMount(async () => {
        const app = document.querySelector('.app');

        new ui.Tooltip({
            theme: 'material',
            rootTarget: app,
            container: app,
            target: '[data-tooltip]',
            direction: ui.Tooltip.TooltipArrowPosition.Auto,
            position: ui.Tooltip.TooltipPosition.Top,
            padding: 10,
            animation: true
        });
	});
</script>

<div class="tabs-list">
	<slot></slot>
    <button 
        on:click="{() => addTab()}" 
        data-tooltip="Add a new tab" 
        data-tooltip-position="top"
    >+</button>
</div>

<style>
</style>
