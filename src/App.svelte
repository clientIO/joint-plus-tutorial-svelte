<script lang="ts">
    import { onMount } from 'svelte';
    import { dia, ui, shapes } from '@clientio/rappid/rappid.js';
    import '../node_modules/@clientio/rappid/rappid.css';

    let ref;

    onMount(() => {
        const graph = new dia.Graph({}, { cellNamespace: shapes });
    
        const paper = new dia.Paper({
            model: graph,
            background: {
                color: '#F8F9FA',
            },
            frozen: true,
            async: true,
            sorting: dia.Paper.sorting.APPROX,
            cellViewNamespace: shapes,
        });
        
            const scroller = new ui.PaperScroller({
            paper,
            autoResizePaper: true,
            cursor: 'grab',
        });
    
        ref.appendChild(scroller.el);
        scroller.render().center();
    
        const rect = new shapes.standard.Rectangle({
            position: { x: 100, y: 100 },
            size: { width: 100, height: 50 },
            attrs: {
                label: {
                    text: 'Hello World',
                },
            },
        });
    
        graph.addCell(rect);
    
        paper.unfreeze();
    });
</script>

<main bind:this={ref} class="app"></main>

<style>
</style>
