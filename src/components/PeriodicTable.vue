<script setup lang="ts">
import elements from '@/data/periodic-table-elements.json'
import ElementItem from '@/components/ElementItem.vue'
import { ref } from 'vue'

const isTableInverted = ref(false)
function invertTable() {
  isTableInverted.value = !isTableInverted.value
}
</script>

<template>
  <div class="wrapper">
    <div class="periodic-table" :class="{ inverted: isTableInverted }">
      <ElementItem v-for="element in elements" :key="element.atomicNumber" :element="element" />
    </div>
    <button @click="invertTable" class="invert-button">Invert</button>
  </div>
</template>

<style scoped>
.wrapper {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.periodic-table {
  display: grid;
  gap: 8px;
  margin-bottom: 24px;
}
.periodic-table.inverted {
  transform: rotate(180deg);
}
.periodic-table.inverted:deep(.element) {
  transform: rotate(180deg);
}
.invert-button {
  padding: 12px 24px;
  min-height: 42px;
  margin: 0 auto;
  display: block;
  background: #cecece;
  border-radius: 5px;
  border: 1px solid #000;
  font-weight: bold;
  cursor: pointer;
}
.invert-button:hover {
  background: #afafaf;
}
</style>
