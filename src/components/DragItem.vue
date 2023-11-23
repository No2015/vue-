<template>
  <div class="drag-item" :style="style" :class="{move: item.moveState, drag: item.dragState}" draggable="true" @dragstart="onDrag" :data-dragid="item.id">
    <slot></slot>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: 'DragItem',
  props: {
    item: {
      type: Object,
      default: () => {}
    },
    paths: {
      type: Array,
      default: () => []
    },
  },
  data () {
    return {
     }
  },
  computed: {
    style({item, paths}) {
      return {
        width: paths[item.path] + 'px',
        height: item.height + 'px',
      }
    }
  },
  methods: {
    onDrag (e) {
      this.item.move = true
      this.item.dragState = true
      e.dataTransfer.setData('dragid', e.target.dataset.dragid)
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.drag-item {
  padding: 10px;
  /* height: 60px; */
  /* width: 120px; */
  border: 1px solid #ccc;
  margin: 10px;
  cursor: move;
}
.move {
  border: 1px dashed #ccc;
}
.drag {
  border: 1px dashed #ff5a0c;
}
</style>
