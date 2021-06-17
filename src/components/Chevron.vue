<template>
  <div
    role="button"
    tabindex="1"
    :aria-label="modifier"
    :class="`gallery ${modifier}`"
    @click="action(modifier)"
    @keypress.enter="action(modifier)"
  >
    <span :class="`chevron ${modifier}`">{{ modifier === "left" ? "PREV" : "NEXT" }}</span>
  </div>
</template>

<script>
export default {
  name: "Chevron",
  props: {
    action: {
      type: Function,
      required: true,
    },
    modifier: {
      type: String,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.gallery {
  width: 120px;
  height: 44px;
  background: #42b883;
  border-radius: 5px;

  &.right {
    padding-right: 10px;
  }

  &.left {
    padding-left: 10px;
  }

  .chevron {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 22px;
    font-weight: bold;
    width: 100%;
    height: 100%;
    position: relative;
    cursor: pointer;

    &:before {
      border-style: solid;
      border-width: 0.25em 0.25em 0 0;
      content: "";
      display: inline-block;
      height: 10px;
      top: 14px;
      position: absolute;
      transform: rotate(-45deg);
      vertical-align: top;
      width: 10px;
    }

    &.right {
      &:before {
        right: 10px;
        transform: rotate(45deg);
      }
    }

    &.left {
      &:before {
        left: 10px;
        transform: rotate(-135deg);
      }
    }
  }
}
</style>
