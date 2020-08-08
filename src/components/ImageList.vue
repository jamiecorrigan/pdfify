<template>
  <Draggable
    v-model="computedImages"
  >
    <VCard
      v-for="(image, index) in images"
      :key="index"
      flat
      tile
    >
      <VCardSubtitle>
        {{ image.name }}
      </VCardSubtitle>
    </VCard>
  </Draggable>
</template>

<script>
import Draggable from 'vuedraggable';

export default {
  name: 'ImageList',
  components: {
    Draggable,
  },
  props: {
    images: { type: Array, required: true },
  },
  computed: {
    computedImages: {
      get() {
        return this.images;
      },
      set(val) {
        this.$emit('update:images', val)
      },
    },
  },
};
</script>
