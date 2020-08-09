<template>
  <VCard>
    <VCardText>
      <Draggable v-model="computedImages">
        <VCard
          v-for="(image, index) in images"
          :key="index"
          flat
          tile
          outlined
        >
          <VCardText>
            <div class="d-flex align-center">
              <VIcon>
                drag_handle
              </VIcon>
              <div class="ml-3 image-name">
                {{ image.name }}
              </div>
              <VSpacer />
              <VBtn
                color="primary"
                icon
                @click="$emit('preview', image)"
              >
                <VIcon>
                  visibility
                </VIcon>
              </VBtn>
              <VBtn
                class="ml-1"
                color="error"
                icon
                @click="deleteImage(index)"
              >
                <VIcon>
                  delete
                </VIcon>
              </VBtn>
            </div>
          </VCardText>
        </VCard>
      </Draggable>
    </VCardText>
  </VCard>
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
  methods: {
    deleteImage(index) {
      this.images.splice(index, 1);
    },
  },
};
</script>
