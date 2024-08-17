<template>
  <div
    class="draggable-item"
    @mousedown="startDrag"
    :style="{ left: `${localItem.x}px`, top: `${localItem.y}px`, width: `${localItem.width}px`, height: `${localItem.height}px` }"
  >
    <span>{{ localItem.props.text }}</span>
  </div>
</template>

<script>
export default {
  name: 'DraggableItem',
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      localItem: { ...this.item }, // Make a copy of the item prop
      isDragging: false,
      startX: 0,
      startY: 0,
      initialX: this.item.x,
      initialY: this.item.y
    };
  },
  methods: {
    startDrag(e) {
      e.preventDefault();
      this.isDragging = true;
      this.startX = e.clientX;
      this.startY = e.clientY;

      document.addEventListener('mousemove', this.drag);
      document.addEventListener('mouseup', this.stopDrag);
    },
    drag(e) {

console.log('dragging')
console.log(this.isDragging)
      if (this.isDragging) {
        const dx = e.clientX - this.startX;
        const dy = e.clientY - this.startY;

        console.log('dx => dy', dx, dy)

        // Update localItem instead of item
        this.localItem.x = this.initialX + dx;
        this.localItem.y = this.initialY + dy;

        // Emit an update event with the updated localItem
        this.$emit('update', this.localItem);
      }
    },
    stopDrag() {
      this.isDragging = false;
      this.initialX = this.localItem.x;
      this.initialY = this.localItem.y;

      document.removeEventListener('mousemove', this.drag);
      document.removeEventListener('mouseup', this.stopDrag);
    }
  }
};
</script>

<style scoped>
.draggable-item {
  position: absolute;
  border: 1px solid #000;
  background-color: #fff;
  cursor: move;
}
</style>
