<template>
  <div
    v-bind:class="['employees-editing-window', {'employees-editing-window__fadeIn': isActive}, {'employees-editing-window__fadeOut': !isActive}]"
  >
    <div class="employees-editing-window__content">
      <form @submit="handleSave">
        <h2 class="employees-editing-window__title">Employee edition</h2>
        <div class="employees-editing-window__hr">
          <div></div>
          <div></div>
          <div></div>
        </div>
        <TextInput label="Full Name" name="name" :value="employee.name" @change="handleChange" />
        <TextInput
          label="Street"
          name="street"
          :value="employee.address.street"
          @change="handleChange"
        />
        <TextInput
          label="Suite"
          name="suite"
          :value="employee.address.suite"
          @change="handleChange"
        />
        <TextInput label="City" name="city" :value="employee.address.city" @change="handleChange" />
        <TextInput label="Phone" name="phone" :value="employee.phone" @change="handleChange" />
        <TextInput label="Email" name="email" :value="employee.email" @change="handleChange" />
        <div class="employees-editing-window__buttons-container">
          <button
            type="button"
            class="employees-editing-window__button"
            @click="handleCancel"
          >Cancel</button>
          <button type="submit" class="employees-editing-window__button">Save</button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import TextInput from "@components/EmployeesList/TextInput";

export default {
  data() {
    return {
      localEmployee: Object.assign({}, this.employee),
      localEmployeeAdress: Object.assign({}, this.employee.address), // without it it updates orginal state
      isActive: true
    };
  },
  components: {
    TextInput
  },
  props: {
    employee: Object,
    save: Function,
    cancel: Function,
    method: { type: Function }
  },
  methods: {
    handleChange() {
      const { value, name } = event.target;
      if (name === "street" || name === "suite" || name === "city") {
        this.localEmployeeAdress[event.target.name] = value;
      } else {
        this.localEmployee[event.target.name] = value;
      }
    },
    handleSave(e) {
      e.preventDefault();
      this.localEmployee.address = this.localEmployeeAdress;
      this.isActive = false;
      this.$emit("save", this.localEmployee);
    },
    handleCancel() {
      this.isActive = false;
      this.$emit("cancel");
    }
  }
};
</script>
<style lang="scss" scoped>
.employees-editing-window {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 100;
  overflow-x: hidden;
  overflow-y: auto;
  background-color: rgba(255, 255, 255, 0.692);

  &__content {
    position: absolute;
    top: 7%;
    left: 5%;
    right: 5%;
    height: auto;
    z-index: 100;
    background-color: #ffffff;
    box-shadow: 0 0 15px #ced0d0;
    color: #000000;
    border-radius: 0.3em;
    transition-duration: 300ms;
    margin: 1.8em auto;
    padding: 1em;
    @media screen and (min-width: 420px) {
      left: 10%;
      right: 10%;
    }
    @media screen and (min-width: 620px) {
      left: 15%;
      right: 15%;
    }
    @media screen and (min-width: 840px) {
      left: 20%;
      right: 20%;
    }
    @media screen and (min-width: 1080px) {
      top: 15%;
      left: 25%;
      right: 25%;
    }
  }

  &__title {
    text-align: center;
    font-size: 1.7em;
    margin: 1em 0;
  }

  &__hr {
    display: flex;
    box-shadow: 0 0 15px #ced0d0;
    margin-bottom: 2em;

    div {
      height: 2px;
      width: 100%;
      background-color: #fb8602;
    }
    div:first-of-type {
      background-color: #52be30;
    }
    div:last-of-type {
      background-color: #f74a00;
    }
  }

  &__buttons-container {
    padding: 0.9em 1em;
    text-align: right;
  }

  &__button {
    font-size: 1.2em;

    background-color: transparent;
    border: 1px solid #000000;
    color: #000000;
    border-radius: 0.2em;
    transition-duration: 300ms;
    padding: 0.25em 0.5em;
    cursor: pointer;
    &:hover:not(:disabled) {
      color: white;
      background-color: #000000;
    }
    &:first-of-type {
      margin-right: 0.3em;
    }
  }

  &__fadeIn {
    animation: fadeIn 0.3s ease-in;
  }
  &__fadeOut {
    animation: fadeOut 0.3s ease-out;
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  @keyframes fadeOut {
    from {
      opacity: 1;
    }
    to {
      opacity: 0;
    }
  }
}
</style>