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
            <ImageList :images.sync="images" />
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
import ImageList from '@/components/ImageList';

export default {
  name: 'App',
  components: {
    ImageInput,
    ImageList,
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
