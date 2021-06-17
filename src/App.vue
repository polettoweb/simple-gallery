<template>
  <div class="header">
    <img alt="Vue logo" src="./assets/logo.png" />
  </div>
  <div v-if="loading" class="spinner-container">
    <Spinner />
  </div>
  <div v-else-if="errorMessage !== ''" class="error-container">
    <p>{{ errorMessage }}</p>
  </div>
  <template v-else>
    <div class="controls">
      <Chevron :action="changeGallery" modifier="left" />
      <div class="gallery-name">
        <h1>Gallery {{ albumId }}</h1>
      </div>
      <Chevron :action="changeGallery" modifier="right" />
    </div>
    <Gallery :photos="photos" />
  </template>
</template>

<script>
import Gallery from "./components/Gallery.vue";
import Chevron from "./components/Chevron.vue";
import Spinner from "./components/Spinner.vue";

export default {
  name: "App",
  components: {
    Gallery,
    Chevron,
    Spinner,
  },
  data() {
    return {
      photos: [],
      albumId: 1,
      loading: true,
      errorMessage: "",
    };
  },
  mounted() {
    this.loadGalleries();
  },
  methods: {
    async loadGalleries() {
      this.loading = true;
      this.errorMessage = "";

      try {
        const API = `https://jsonplaceholder.typicode.com/photos?&_limit=30&albumId=${this.albumId}`;
        const res = await fetch(API);
        if (!res.ok) {
          this.loading = false;
          if (res.status === 404) {
            throw new Error("ERROR: The provided URL was not found");
          } else {
            throw new Error("ERROR: Something went wrong please try again");
          }
        }
        const data = await res.json();
        this.photos = data;
        this.loading = false;
      } catch (err) {
        this.errorMessage = err.message;
      }
    },
    changeGallery(modifier) {
      if (modifier === "left" && this.albumId <= 1) return;
      modifier === "right" && this.albumId++;
      modifier === "left" && this.albumId--;
      this.loadGalleries();
    },
  },
};
</script>

<style>
body {
  font-family: Helvetica, Arial, sans-serif;
  background: black;
}

.header {
  display: flex;
  justify-content: center;
  padding: 16px 0;
}

.controls {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
  padding: 16px 0;
}

.gallery-name {
  padding: 0 20px;
  color: #42b883;
  text-transform: uppercase;
}

.spinner-container,
.error-container {
  color: red;
  font-size: 24px;
  width: 100%;
  padding: 80px 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
