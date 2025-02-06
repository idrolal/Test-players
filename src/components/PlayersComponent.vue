<template>
  <section class="player-wrapper">
    <div class="tab">
      <div class="tab-header">
        <div
          @click="changeTab('CreatePlayer')"
          :class="{ 'active-tab': component === 'CreatePlayer' }"
        >
          <p>Добавить нового игрока</p>
        </div>
        <div
          @click="changeTab('EditPlayers')"
          :class="{
            'active-tab': component === 'EditPlayers',
            'disabled-tab': !playersList.length,
          }"
        >
          <p>Редактирование игроков</p>
        </div>
      </div>

      <div class="tab-content">
        <keep-alive>
          <component
            :is="activeTab"
            :playersList="playersList"
            @createdPlayers="createdPlayers"
            @updatePlayer="updatePlayer"
          />
        </keep-alive>
      </div>
    </div>

    <div class="rating">
      <RatingPlayer :playersList="playersList" />
    </div>
  </section>
</template>

<script setup>
import RatingPlayer from './RatingPlayer.vue';
import CreatePlayer from './CreatePlayer.vue';
import EditPlayers from './EditPlayers.vue';
import { ref, computed } from 'vue';

const component = ref('CreatePlayer');
const playersList = ref([]);

const activeTab = computed(
  () =>
    ({
      CreatePlayer,
      EditPlayers,
    }[component.value])
);

const changeTab = (tab) => {
  component.value = tab;
};

const updatePlayer = ({ player, idx }) => {
  playersList.value[idx] = player;
};

const createdPlayers = (player) => {
  playersList.value.push(player);
};
</script>

<style scoped lang="scss">
.player-wrapper {
  width: 100%;
  display: flex;
  justify-content: space-between;
  height: 100%;
  background-color: white;
  border-radius: 8px;


  & > div {
    flex: 1;
    max-width: 50%;
    height: 100%;
  }

  .tab {
    display: flex;
    flex-direction: column;
    padding: 10px 18px;
    border-right: 1px solid rgba(166, 149, 149, 0.2);
    box-shadow: 12px 0px 16px -3px rgba(34, 60, 80, 0.2);

    .tab-header {
      display: flex;
      gap: 6px;
      padding: 4px 6px;
      overflow-x: auto;
      font-size: 18px;
      background-color: white;
      min-height: 36px;

      div {
        cursor: pointer;
        padding-inline: 4px;
        transition: all 0.3s;
        border-bottom: 1px solid transparent;

        &.active-tab {
          border-color: rgba(41, 41, 228, 0.558);
          color: rgba(41, 41, 228, 0.558);
        }

        &.disabled-tab {
          cursor: not-allowed;
          color: #cec8c8;
          pointer-events: none;
        }
      }
    }

    .tab-content {
      padding: 20px 8px;
      overflow-y: auto;
      background-color: rgba(214, 214, 252, 0.154);
    }
  }
}
</style>
