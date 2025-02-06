<template>
  <div class="row">
    <input
      id="name"
      type="text"
      v-model="players_name"
      placeholder="Имя"
      :class="{
        invalid: errors.name,
      }"
    />
    <input
      type="number"
      class="life"
      :min="1"
      v-model="players_life"
      placeholder="Жизней"
      :class="{
        invalid: errors.life,
      }"
    />
    <button type="button" v-on:click="createPlayer">Создать</button>
  </div>
  <p v-show="errors.life || errors.name" class="error-message">
    {{ errors.name || errors.life }}
  </p>
</template>

<script>
export default {
  name: 'CreatePlayer',

  data() {
    return {
      players_name: '',
      players_life: '',
      errors: {
        name: false,
        life: false,
      },
    };
  },
  methods: {
    validate() {
      let isValid = true;

      if (this.players_name.trim() === '' || this.players_name === undefined) {
        this.errors.name = 'Укажите имя';
        isValid = false;
      } else {
        this.errors.name = false;
      }

      if (!this.players_life || this.players_life < 1) {
        this.errors.life =
          this.players_life === ''
            ? 'Укажите количество жизней'
            : 'Значение не может быть меньше нуля';
        isValid = false;
      } else {
        this.errors.life = false;
      }

      return isValid;
    },
    createPlayer() {
      if (!this.validate()) {
        return;
      }
      this.$emit('createdPlayers', {
        name: this.players_name,
        life: this.players_life,
        id: +new Date(),
      });

      this.players_name = '';
      this.players_life = '';
    },
  },
};
</script>

<style scoped lang="scss">
.row {
  display: flex;
  gap: 12px;

  input {
    width: 100%;
    min-width: 70px;
  
    &.life {
      width: 100px;
    }
  }
}

.error-message {
  color: red;
}
</style>
