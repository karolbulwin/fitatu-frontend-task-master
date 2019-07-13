<template>
  <button class="employees-list__edit-button" @click="handleClick">{{text}}</button>
</template>
<script>
export default {
  props: ["text"],
  methods: {
    handleClick() {
      this.$emit("click");
    }
  }
};
</script>
<style lang="scss" scoped>
.employees-list__edit-button {
  background-color: transparent;
  border: 1px solid #000000;
  color: #000000;
  border-radius: 0.2em;
  transition-duration: 300ms;
  padding: 0.3em 0.7em;
  cursor: pointer;
  &:hover {
    color: white;
    background-color: #000000;
  }
}
</style>