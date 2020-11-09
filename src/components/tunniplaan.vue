<template>
  <h1>Tunniplaan</h1>
  <select name="" id="" v-model="active" @change="getTimeTable">
    <option value="0" selected>Vali ruhm</option>
    <option v-for="group in groups" :key="group.groupId" :value="group.groupId">
      {{ group.groupCode }}
    </option>
  </select>
</template>

<script>
import { computed, onMounted, ref } from "vue";
import * as dayjs from "dayjs";
export default {
  setup() {
    const groups = ref([]);
    const active = ref(0);
    const timeTable = ref([]);

    const days = computed(() => {
      if (condition) {
      }
      return timeTable.timeTableEvents.map((item) => {
        return item;
      });
    });

    const getGroups = async () => {
      groups.value = await (
        await fetch("https://be.ta19heinsoo.itmajakas.ee/api/groups")
      ).json();
    };

    const getTimeTable = async () => {
      timeTable.value = await (
        await fetch(
          `https://be.ta19heinsoo.itmajakas.ee/api/lessons/groups=${active.value}&weeks=10`
        )
      ).json();
    };

    onMounted(getGroups);
    return {
      groups,
      active,
      getTimeTable,
      timeTable,
      days,
    };
  },
};
</script>

<style>
</style>
