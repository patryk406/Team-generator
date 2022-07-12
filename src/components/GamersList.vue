<script setup lang="ts">
defineProps<{
  availableGamers: Array<String>;
  checkedPlayers: Array<String>;
}>();
defineEmits<{ e: "handleCheck"; val: string }>();
</script>

<template>
  <div class="container">
    <div
      class="person"
      v-for="(player, index) in availableGamers"
      :key="index"
      @click="$emit('handleCheck', player)"
    >
      <div
        class="checkbox"
        :class="{
          checked: player === checkedPlayers.find((el) => el === player),
        }"
      ></div>
      <span class="name">{{ player }}</span>
    </div>
  </div>
</template>

<style scoped>
.person {
  min-width: 120px;
  height: 40px;
  display: flex;
  align-items: center;
  border: 2px solid #000;
  border-radius: 8px;
  margin: 10px 0;
  padding: 10px;
  cursor: pointer;
}
.checkbox {
  height: 15px;
  width: 15px;
  border: 1px solid white;
  border-radius: 4px;
  margin-right: 10px;
}
.checked {
  background-color: white;
}
</style>
