<template>
    <div class="drag-box" @dragover="onDragOver" @drop="onDrop">
      <slot></slot>
    </div>
</template>

<script>
/* eslint-disable */
export default {
  name: 'DragBox',
  props: {
    list: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
    }
  },
  methods: {
    onDragOver (e) {
      // console.log(e)
      e.preventDefault()
      const ele = e.composedPath().find(ele => ele.dataset && ele.dataset.dragid)
      if (ele) {
        const dragid = ele.dataset.dragid
        const move = this.list.findIndex(item => item.id == dragid)
        if (!this.list[move].moveState) {
          this.list.forEach(item => {
            item.moveState = false
          })
          this.list[move].moveState = true
        }
      } else {
        this.list.forEach(item => {
          item.moveState = false
        })
      }
    },
    onDrop (e) {
      const start = this.list.findIndex(el => el.dragState)
      const end = this.list.findIndex(el => el.moveState)
      this.list.forEach(item => {
        item.moveState = false
        item.dragState = false
      })
      if (start > -1 && end > -1 && start !== end) {
        const min = Math.min(start, end)
        const max = Math.max(start, end)
        const minEl = this.list[min]
        const maxEl = this.list[max]
        const path = minEl.path
        minEl.path = maxEl.path
        maxEl.path = path
        this.list[min] = maxEl
        this.list[max] = minEl
        console.log(`>>> 交换${min}和${max}`)
      }
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.drag-box {
  position: relative;
  z-index: 1;
}
.drag-box::before {
  content: "";
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  z-index: -1;
}
</style>
