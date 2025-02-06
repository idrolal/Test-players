<template>
  <PlayersComponent />
</template>

<script>
import PlayersComponent from './components/PlayersComponent.vue';
export default {
  name: 'App',
  components: {
    PlayersComponent,
  },
  created() {},
};
</script>

<style lang="scss">
input {
  padding: 9px 16px;
  outline: none;
  border-radius: 4px;
  border: 1px solid #979292;
  cursor: auto;

  &.invalid {
    border-color: red;
  }

  &::placeholder {
    color: #cec8c8;
  }

  &:not(&:disabled) {
    &:focus,
    &:hover {
      background-color: rgba(214, 214, 252, 0.154);
      border-color: rgba(41, 41, 228, 0.558);
    }
  }

  &:-webkit-autofill,
  &:-webkit-autofill:hover,
  &:-webkit-autofill:focus,
  &:-webkit-autofill:active {
    transition: background-color 5000s ease-in-out 0s;
  }

  &[type='number']::-webkit-outer-spin-button,
  &[type='number']::-webkit-inner-spin-button {
    -webkit-appearance: none; // Yeah, yeah everybody write about it
  }

  &[type='number'],
  &[type='number']:hover,
  &[type='number']:focus {
    appearance: none;
    -moz-appearance: textfield;
  }

  &:disabled {
    background-color: rgba(151, 146, 146, 0.12);
    color: #979292;
  }
}

button {
  background-color: #fff;
  border: 1px solid #dbdbdb;
  color: #363636;
  cursor: pointer;
  text-align: center;
  white-space: nowrap;
  outline: none;
  border-radius: 4px;
  box-shadow: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
  vertical-align: top;

  &:hover {
    border-color: #9d9c9c;
  }
}
* {
  margin: 0;
}
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
  margin: 0;
  padding: 20px;
  background-color: rgba(166, 149, 149, 0.2);
}
</style>
