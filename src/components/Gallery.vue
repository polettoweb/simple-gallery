<template>
  <div class="container">
    <div tabindex="1" class="photo" v-for="photo in photos" :key="photo.id">
      <img :src="photo.url" :alt="photo.title" />
      <div class="caption">
        <p>{{ photo.title }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Gallery",
  props: {
    photos: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  width: 100%;
  margin: 0 auto 80px;
  max-width: 1200px;
}

.photo {
  position: relative;
  width: 200px;
  height: 200px;

  img {
    width: 100%;
    height: 100%;
  }
}

.caption {
  opacity: 0;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  position: absolute;
  bottom: 0;
  padding: 10px;
  background-color: rgba(0, 0, 0, 0.2);
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  transition: all 0.3s ease-in;

  &:hover {
    opacity: 1;
  }

  p {
    text-align: center;
  }
}
</style>
