<template>
  <VCard :loading="loading">
    <VCardTitle>
      Load Images
    </VCardTitle>
    <VCardText>
      <div class="d-flex align-center">
        <VFileInput
          v-model="files"
          :disabled="loading"
          label="Images"
          accept="image/*"
          multiple
          hide-details
          dense
        />
        <VBtn
          :disabled="loading || !files.length"
          color="success"
          class="ml-4"
          fab
          x-small
          @click="commit"
        >
          <VIcon>add</VIcon>
        </VBtn>
      </div>
    </VCardText>
  </VCard>
</template>

<script>
export default {
  name: 'ImageInput',
  data: () => ({
    files: [],
    loading: false,
  }),
  methods: {
    async commit() {
      if (this.loading) return;
      this.loading = true;

      try {
        const images = await Promise.all(this.files.map(this.getImage));
        this.$emit('add', images);
      } catch (error) {
        console.log(error);
      }

      this.loading = false;
      this.files = [];
    },
    getImage(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => resolve({ name: file.name, data: reader.result });
        reader.onerror = error => reject(error);
      });
    }
  },
};
</script>
