<script lang="ts">
  import { onMount } from 'svelte';
  import { dia, ui, shapes } from '@clientio/rappid';
  import '../node_modules/@clientio/rappid/rappid.css';

  let ref;

  onMount(async () => {
    const namespace = shapes;

    const graph = new dia.Graph({}, { cellNamespace: namespace });

    const paper = new dia.Paper({
      model: graph,
      background: {
        color: '#F8F9FA',
      },
      frozen: true,
      async: true,
      sorting: dia.Paper.sorting.Approx,
      cellViewNamespace: namespace,
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

<main bind:this={ref} class="app" />

<style>
</style>
