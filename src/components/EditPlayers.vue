<template>
  <div class="form-wrapper">
    <div v-for="(item, idx) in usersLife" :key="item.id" class="row">
      <input
        @change="updateDataPlayer(item, idx)"
        v-model="item.name"
        :minlength="1"
        placeholder="Имя"
      />

      <div class="row-action">
        <input
          class="lifeCount"
          v-model="item.life"
          type="number"
          :min="1"
          @change="updateDataPlayer(item, idx)"
          :disabled="item.life <= 1"
          :class="{
            invalid: item.life < 1,
          }"
        />

        <div>
          <button type="button" class="button" @click="plusLife(item, idx)">
            +
          </button>
          <button
            type="button"
            class="button"
            @click="minusLife(item, idx)"
            :disabled="item.life <= 1"
          >
            -
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EditPlayers',

  props: {
    playersList: {
      type: Array,
      default: () => [],
    },
  },

  computed: {
    usersLife() {
      return this.playersList.map((player) => ({ ...player }));
    },
  },

  methods: {
    updateDataPlayer(item, idx) {
      if (item.name.trim().length && item.life > 1) {
        this.updatePlayer(item, idx);
      }
    },
    plusLife(item, idx) {
      item.life += 1;
      this.updatePlayer(item, idx);
    },

    minusLife(item, idx) {
      if (item.life > 1) {
        item.life -= 1;
        this.updatePlayer(item, idx);
      }
    },

    updatePlayer(player, idx) {
      this.$emit('updatePlayer', { player, idx });
    },
  },
};
</script>

<style lang="scss" scoped>
.form-wrapper {
  display: flex;
  align-items: start;
  flex-direction: column;
  gap: 20px;

  .row {
    display: flex;
    align-items: center;
    gap: 12px;
    width: 100%;

    input {
      width: 100%;
    }

    .button {
      width: 24px;
      height: 24px;
    }

    .row-action {
      display: flex;
      align-items: center;
      justify-content: end;
    }
  }
}
</style>
