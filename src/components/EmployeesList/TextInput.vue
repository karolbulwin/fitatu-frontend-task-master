<template>
  <div class="text-input">
    <label :for="name">{{label}}</label>
    <input
      :id="name"
      v-bind:name="name"
      class="text-input__input"
      v-bind:value="value"
      v-on:change="$emit('change', $event.target)"
      placeholder="This can not be empty"
      required
    />
    <span class="text-input__underline" />
  </div>
</template>
<script>
export default {
  data() {
    return {
      error: false
    };
  },
  props: ["label", "name", "value"]
};
</script>
<style lang="scss" scoped>
.text-input {
  margin: 0.8em auto;
  line-height: 1em;
  font-size: 1em;
  width: 95%;
  position: relative;

  &__input {
    width: 100%;
    height: 2em;
    background-color: transparent;
    border: none;
    border-bottom: 2px solid #f7f8f9;
    color: #000000;
    transition-duration: 300ms;
    padding: 0.25em 0.5em;
    font-size: 1.2em;
    cursor: pointer;
    &:focus {
      outline: none;
    }
  }

  &__underline {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 2px;
    background-color: darken(#f7f8f9, 20%);
    transform-origin: bottom right;
    transform: scaleX(0);
    transition: transform 0.5s ease;
  }

  &__input:focus ~ &__underline {
    transform-origin: bottom left;
    transform: scaleX(1);
  }
}
</style>