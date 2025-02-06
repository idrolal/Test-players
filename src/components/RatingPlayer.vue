<template>
  <h2>Рейтинг</h2>
  <div class="rating-table">
    <table v-if="playersList.length">
      <colgroup>
        <col :style="`min-width: 20px; max-width: 50px`" />
        <col />
        <col :style="`max-width: 100px;`" />
      </colgroup>
      <thead>
        <tr>
          <th></th>
          <th>Имя</th>
          <th>Жизни</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(item, index) in rating" :key="item.id">
          <th>{{ index + 1 }}</th>
          <td>
            <b>{{ item.name }}</b>
          </td>
          <td>
            {{ item.life }}
          </td>
        </tr>
      </tbody>
    </table>
    <p v-else>Список игроков пуст</p>
  </div>
</template>

<script setup>
import { computed, defineProps } from 'vue';

const props = defineProps({
  playersList: { type: Array, default: () => [] },
});

const rating = computed(() => {
  return [...props.playersList].sort((a, b) => b.life - a.life);
});
</script>

<style lang="scss" scoped>
h2 {
  color: rgba(41, 41, 228, 0.558);
  margin-top: 10px;
}
.rating-table {
  overflow: auto;
  width: 100%;
  height: 100%;
  margin-top: 20px;

  p {
    color: #979292;
    font-size: 18px;
    margin: 0 auto;
  }

  table {
    width: 100%;
    overflow-y: auto;
    border-collapse: collapse;

    th {
      color: rgba(41, 41, 228, 0.558);
    }

    td {
      padding: 9px 16px;
      height: 24px;
    }

    tbody {
      tr {
        border-bottom: 1px solid rgba(214, 214, 252, 0.154);
        th {
          border-right: 1px solid rgba(214, 214, 252, 0.154);
        }

        &:nth-child(2n) {
          background-color: rgba(176, 176, 239, 0.154);
        }
      }
    }
  }
}
</style>
