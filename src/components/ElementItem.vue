<script setup lang="ts">
import { computed } from 'vue'

interface ElementType {
  name: String
  atomicNumber: Number
  symbol: String
  atomicWeight: Number
  block: BlockType
  row: Number
  column: Number
}

enum BlockType {
  b,
  s,
  p,
  f,
  d
}

const ELEMENT_COLORS: any = {
  b: '#9acdff',
  s: '#ff9a9a',
  p: '#fdff8d',
  f: '#9acdff',
  d: '#9cff9a'
}

const props = defineProps<{
  element: ElementType
}>()

const elementBackground = computed(() => {
  return ELEMENT_COLORS[props.element.block]
})
const elementRow = computed(() => {
  return props.element.row
})
const elementColumn = computed(() => {
  return props.element.column
})
</script>

<template>
  <a
    class="element"
    :href="`https://en.wikipedia.org/wiki/${element.name}`"
    target="_blank"
    :title="element.name.toString()"
  >
    <div class="element-number">{{ element.atomicNumber }}</div>
    <div class="element-symbol">{{ element.symbol }}</div>
    <div class="element-name">{{ element.name }}</div>
  </a>
</template>

<style scoped>
.element {
  padding: 5px;
  border-radius: 4px;
  display: grid;
  grid-template-areas:
    'number symbol'
    'name name';
  min-width: 48px;
  grid-template-columns: 1fr auto;
  align-items: center;
  color: #1b1b1b;
  background: v-bind(elementBackground);
  grid-row: v-bind(elementRow);
  grid-column: v-bind(elementColumn);
  font-size: 14px;
  box-shadow: 2px 1px 2px v-bind(elementBackground);
}
.element-number,
.element-symbol {
  font-size: 10px;
  color: #303030;
}
.element-number {
  grid-area: number;
}
.element-symbol {
  grid-area: symbol;
}
.element-name {
  font-weight: bold;
  grid-area: name;
  justify-self: center;
}

@media screen and (max-width: 1850px) {
  .element-name {
    display: none;
  }
  .element-symbol {
    grid-area: name;
    font-weight: bold;
    font-size: 14px;
  }
}
</style>
