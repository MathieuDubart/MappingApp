<template>
  <div>
    <!-- Div pour choisir une image -->
    <div>
      <h2>Choisissez une image :</h2>
      <div v-for="(image, index) in images" :key="index" @click="selectImage(image)">
        <img :src="image" alt="Image" width="50" height="50" />
      </div>
    </div>

    <!-- Div pour afficher l'image choisie et la dupliquer -->
    <div v-if="selectedImage">
      <h2>Image choisie :</h2>
      <div ref="draggableContainer">
        <draggable v-model="imagesOnPage" :options="dragOptions">
          <div v-for="(image, index) in imagesOnPage" :key="index">
            <img :src="image" alt="Image" width="50" height="50" />
          </div>
        </draggable>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import VueDraggableNext  from 'vue-draggable-next';

export default {
  components: {
    draggable: VueDraggableNext,
  },
  data() {
    return {
      images: ['/src/assets/stickers/sticker-1.png', '/src/assets/stickers/sticker-2.png', '/src/assets/stickers/sticker-3.png'], // Ajoutez vos URLs d'images
      selectedImage: null,
      imagesOnPage: [],
      dragOptions: {
        onStart: () => {
          // Bloquer le déplacement de l'image originale
          this.$refs.draggableContainer.$el.style.pointerEvents = 'none';
        },
        onStop: () => {
          // Réactiver le déplacement de l'image originale
          this.$refs.draggableContainer.$el.style.pointerEvents = 'auto';
        },
      },
    };
  },
  methods: {
    selectImage(image) {
      this.selectedImage = image;
      // Dupliquer l'image sélectionnée
      this.imagesOnPage.push(image);
    },
  },
};
</script>

<style>
/* Ajoutez du style CSS au besoin */
</style>
