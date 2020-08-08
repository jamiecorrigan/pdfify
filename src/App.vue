<template>
  <VApp>
    <VMain>
      <VContainer>
        <VRow>
          <VCol cols="12">
            <ImageInput @add="addImages" />
          </VCol>
        </VRow>
        <VRow>
          <VCol cols="12">
            {{ images.map((f) => f.name) }}
          </VCol>
        </VRow>
        <VRow>
          <VCol cols="12">
            <VBtn @click="clearImages">
              Clear All
            </VBtn>
          </VCol>
        </VRow>
      </VContainer>
    </VMain>
  </VApp>
</template>

<script>
import ImageInput from '@/components/ImageInput';

export default {
  name: 'App',
  components: {
    ImageInput,
  },
  data: () => ({
    images: []
  }),
  methods: {
    addImages(newImages) {
      this.images = this.images.concat(newImages);
    },
    clearImages() {
      this.images = [];
    },
  },
};
</script>
