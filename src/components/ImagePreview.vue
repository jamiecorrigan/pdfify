<template>
  <VDialog
    v-model="visible"
    :width="520"
  >
    <VCard>
      <VCardTitle>
        Image Preview
      </VCardTitle>
      <VCardText>
        <VImg
          v-if="image"
          :src="image.data"
          contain
        />
      </VCardText>
    </VCard>
  </VDialog>
</template>

<script>
export default {
  name: 'ImagePreview',
  props: {
    image: { validator: (val) => val == null || val.constructor == Object, required: true },
  },
  computed: {
    visible: {
      get() {
        return this.image != null;
      },
      set(val) {
        this.$emit('update:image', null);
      },
    },
  },
};
</script>
