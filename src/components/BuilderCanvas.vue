<template>
  <div class="builder-canvas" @drop="onDrop" @dragover.prevent>
    <draggable-item
      v-for="(item, index) in items"
      :key="index"
      :item="item"
      @update="updateItem"
    />
  </div>
</template>

<script>
import DraggableItem from './DraggableItem.vue';

export default {
  name: 'BuilderCanvas',
  components: {
    DraggableItem
  },
  data() {
    return {
      items: []
    };
  },
  methods: {
    onDrop(e) {
      console.log('Drop event received');
      e.preventDefault();
      const type = e.dataTransfer.getData('type');
      console.log('Data type:', type);
      const canvasRect = e.currentTarget.getBoundingClientRect();
      const newItem = {
        type,
        x: e.clientX - canvasRect.left,
        y: e.clientY - canvasRect.top,
        width: 100,
        height: 100,
        props: { text: 'Sample Text' }
      };
      this.items.push(newItem);
      console.log('New item added:', newItem);
    },
    updateItem(updatedItem) {
      const index = this.items.findIndex(item => item === updatedItem);
      if (index !== -1) {
        this.$set(this.items, index, updatedItem);
      }
    }
  }
};
</script>

<style scoped>
.builder-canvas {
  position: relative;
  width: 100%;
  height: 100vh;
  background-color: #f0f0f0;
  border: 2px dashed #ddd;
}
</style>
