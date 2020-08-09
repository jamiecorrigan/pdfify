<template>
  <VApp>
    <VMain>
      <VContainer>
        <VRow>
          <VCol cols="12">
            <ImageInput
              @add="addImages"
              @error="addImagesError = true"
            />
          </VCol>
        </VRow>
        <VRow>
          <VCol cols="12">
            <ImageList
              :images.sync="images"
              @preview="showPreview"
            />
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
    <ImagePreview :image.sync="previewImage" />
    <VSnackbar
      v-model="addImagesError"
      color="error"
      top
    >
      Failed to add images.
      <template v-slot:action="{ attrs }">
        <VBtn
          text
          v-bind="attrs"
          @click="addImagesError = false"
        >
          Close
        </VBtn>
      </template>
    </VSnackbar>
  </VApp>
</template>

<script>
import ImageInput from '@/components/ImageInput';
import ImageList from '@/components/ImageList';
import ImagePreview from '@/components/ImagePreview';

export default {
  name: 'App',
  components: {
    ImageInput,
    ImageList,
    ImagePreview,
  },
  data: () => ({
    images: [],
    previewImage: null,
    addImagesError: true,
  }),
  methods: {
    addImages(newImages) {
      this.images = this.images.concat(newImages);
    },
    clearImages() {
      this.images = [];
    },
    showPreview(img) {
      this.previewImage = img;
    },
  },
};
</script>
