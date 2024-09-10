<script setup lang="ts">
import { ref } from "vue";

const periods = ["Today", "This week", "This month"] as const;

type Period = (typeof periods)[number];

const selectedPeriod = ref<Period>("Today");

const selectPeriod = (period: Period) => {
  selectedPeriod.value = period;
};
</script>

<template>
  <nav class="is-primary panel">
    {{ selectedPeriod }}
    <span class="panel-tabs">
      <a
        v-for="period of periods"
        :key="period"
        @click="selectPeriod(period)"
        >{{ period }}</a
      >
    </span>
  </nav>
</template>

<style scoped></style>
