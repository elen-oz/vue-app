<script setup lang="ts">
import { ref } from "vue";
import { Post, today, thisWeek, thisMonth } from "../posts.ts";
import { DateTime } from "luxon";

const periods = ["Today", "This week", "This month"] as const;

type Period = (typeof periods)[number];

const selectedPeriod = ref<Period>("Today");

const selectPeriod = (period: Period) => {
  selectedPeriod.value = period;
};

const posts = [today, thisWeek, thisMonth].map((post) => {
  return { ...post, created: DateTime.fromISO(post.created) };
});
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

    <a v-for="post of posts" :key="post.id" class="panel-block">
      <a>{{ post.title }}</a>
      <div>{{ post.created.toFormat("d MMM") }}</div>
    </a>
  </nav>
</template>

<style scoped></style>
