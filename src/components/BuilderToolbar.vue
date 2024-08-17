<template>
  <div class="builder-toolbar">
    <button @click="addElement('text')">Add Text</button>
    <button @click="addElement('image')">Add Image</button>
  </div>
</template>

<script>
export default {
  name: 'BuilderToolbar',
  methods: {
    addElement(type) {
      console.log(`Adding element of type: ${type}`);
      const dataTransfer = new DataTransfer();
      dataTransfer.setData('type', type);
      const dropEvent = new Event('drop', { bubbles: true });
      dropEvent.dataTransfer = dataTransfer;
      document.querySelector('.builder-canvas').dispatchEvent(dropEvent); // Dispatch directly to the canvas
      console.log('Drop event dispatched');
    }
  }
};
</script>

<style scoped>
.builder-toolbar {
  padding: 10px;
  background-color: #ddd;
  display: flex;
  gap: 10px;
}
</style>
