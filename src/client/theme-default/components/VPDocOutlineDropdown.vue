<script setup lang="ts">
import { ref } from 'vue'
import { useData } from '../composables/data'
import { getHeaders, resolveTitle } from '../composables/outline'
import VPDocOutlineItem from './VPDocOutlineItem.vue'
import { onContentUpdated } from 'vitepress'
import VPIconChevronRight from './icons/VPIconChevronRight.vue'

const { frontmatter, theme } = useData()
const open = ref(false)

onContentUpdated(() => {
  open.value = false
})
</script>

<template>
  <div class="VPDocOutlineDropdown">
    <button @click="open = !open" :class="{ open }">
      {{ resolveTitle(theme) }}
      <VPIconChevronRight class="icon" />
    </button>
    <div class="items" v-if="open">
      <VPDocOutlineItem :headers="getHeaders(frontmatter.outline ?? theme.outline)" />
    </div>
  </div>
</template>

<style scoped>
.VPDocOutlineDropdown {
  margin-bottom: 42px;
}

.VPDocOutlineDropdown button {
  display: block;
  font-size: 14px;
  font-weight: 500;
  line-height: 24px;
  color: var(--vp-c-text-2);
  transition: color 0.5s;
  border: 1px solid var(--vp-c-border);
  padding: 4px 12px;
  border-radius: 8px;
}

.VPDocOutlineDropdown button:hover {
  color: var(--vp-c-text-1);
  transition: color 0.25s;
}

.VPDocOutlineDropdown button.open {
  color: var(--vp-c-text-1);
}

.icon {
  display: inline-block;
  vertical-align: middle;
  margin-left: 2px;
  width: 14px;
  height: 14px;
  fill: currentColor;
}

:deep(.outline-link) {
  font-size: 13px;
}

.open > .icon {
  transform: rotate(90deg);
}

.items {
  margin-top: 10px;
  border-left: 1px solid var(--vp-c-divider);
}
</style>
