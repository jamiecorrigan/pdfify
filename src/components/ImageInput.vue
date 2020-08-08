<template>
  <div class="d-flex align-center">
    <VFileInput
      v-model="files"
      label="Images"
      accept="image/*"
      multiple
      hide-details
      dense
    />
    <VBtn
      :disabled="!files.length"
      color="success"
      class="ml-4"
      fab
      x-small
      @click="commit"
    >
      <VIcon>add</VIcon>
    </VBtn>
  </div>
</template>

<script>
export default {
  name: 'ImageInput',
  data: () => ({
    files: []
  }),
  methods: {
    commit() {
      this.$emit('add', this.files);
      this.files = [];
    },
  },
};
</script>
