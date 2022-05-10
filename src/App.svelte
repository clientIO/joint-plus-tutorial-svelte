<script lang="ts">
    import { onMount } from 'svelte';
    import { dia, ui, shapes } from '@clientio/rappid';
    import '../node_modules/@clientio/rappid/rappid.css';


    onMount(async () => {

        const main = document.getElementById('app');

        const namespace = shapes;

        const graph = new dia.Graph({}, { cellNamespace: namespace });

        const paper = new dia.Paper({
            el: document.getElementById('root'),
            model: graph,
            background: {
                color: '#F8F9FA',
            },
            frozen: true,
            async: true,
            cellViewNamespace: namespace
        });

        const scroller = new ui.PaperScroller({
            paper,
            autoResizePaper: true,
            cursor: 'grab'
        });

        main.appendChild(scroller.el);
        scroller.render().center(); 


        const rect = new shapes.standard.Rectangle({
            position: { x: 100, y: 100 },
            size: { width: 100, height: 50 },
            attrs: {
                label: {
                    text: 'Hello World'
                }
            }
        });
  
        graph.addCell(rect);
        paper.unfreeze();
    });

</script>
    <main id="app" class="app">

    </main>
<style>
</style>
