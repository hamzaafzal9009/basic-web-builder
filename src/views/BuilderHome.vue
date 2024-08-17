<template>
  <div>
    <builder-toolbar />
    <builder-canvas ref="canvas" />
  </div>
</template>

<script>
import BuilderToolbar from '@/components/BuilderToolbar.vue';
import BuilderCanvas from '@/components/BuilderCanvas.vue';

export default {
  name: 'BuilderHome',
  components: {
    BuilderToolbar,
    BuilderCanvas
  },
  methods: {
    onAddElement(type) {
      const dataTransfer = new DataTransfer();
      dataTransfer.setData('type', type);
      const dropEvent = new Event('drop', { bubbles: true });
      dropEvent.dataTransfer = dataTransfer;
      this.$refs.canvas.$el.dispatchEvent(dropEvent);
    }
  }
};
</script>

<style scoped>
/* Add any additional styling here */
</style>
