<template>
  <div class="hello">
    <!-- <div class="content"></div> -->
    <drag-box :list="list" class="box">
      <div class="drag-list">
        <div class="path" v-for="(path, key) in paths" :key="key">
          <drag-item :paths="paths" :item="item" v-for="(item) in list.filter(item => item.path == key)" :key="item.id">
            <div class="test-box">{{ item.name }}</div>
          </drag-item>
        </div>
      </div>
    </drag-box>
  </div>
</template>

<script>
import DragItem from './DragItem.vue'
import DragBox from './DragBox.vue'
export default {
  name: 'HelloWorld',
  components: {
    DragItem,
    DragBox,
  },
  data() {
    return {
      list: [],
      paths: [300, 500, 400, 200],
    }
  },
  created() {
    this.init()
  },
  methods: {
    init() {
      this.list = new Array(25).fill().map((el, index) => {
        let path = index % 4 //parseInt(Math.random() * 4)
        return {
          id: index,
          name: '测试' + index,
          path,
          height: parseInt(Math.random() * 100 + 30),
        }
      })
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  display: flex;
  justify-content: space-between;
}

.content {
  width: 400px;
  height: 600px;
  border: 1px solid #ddd;
}

.box {
  flex: 1;
}

.drag-list {
  display: flex;
  flex-wrap: wrap;
  /* justify-content: space-between; */
}</style>
