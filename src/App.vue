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
        <template v-if="images.length">
          <VRow>
            <VCol cols="12">
              <VBtn @click="clearImages">
                Clear All
              </VBtn>
              <VBtn
                class="ml-3"
                @click="exportPdf"
              >
                Export To PDF
              </VBtn>
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
        </template>
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
import jsPDF from 'jspdf';
import ImageInput from '@/components/ImageInput';
import ImageList from '@/components/ImageList';
import ImagePreview from '@/components/ImagePreview';

const PDF_PAGE_WIDTH = 210;
const PDF_PAGE_HEIGHT = 297;

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
    addImagesError: false,
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
    exportPdf() {
      const doc = new jsPDF();
      this.images.forEach((image, i) => {
        if (i > 0) doc.addPage();
        doc.addImage(image.data, 'JPEG', 0, 0, PDF_PAGE_WIDTH, PDF_PAGE_HEIGHT);
      });
      doc.save('export.pdf');
    },
  },
};
</script>
