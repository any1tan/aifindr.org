<template>
  <button type="button" aria-label="Search AI tools" :class="compact ? 'header-search-compact' : (expanded ? 'w-full header-search' : 'header-search')" @click="openSearchModal">
    <svg aria-hidden="true" class="search-icon shrink-0" :class="expanded ? 'w-[18px] h-[18px]' : ''" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" width="13" height="13">
      <circle cx="11" cy="11" r="8" />
      <path d="M21 21l-4.35-4.35" />
    </svg>
    <span v-if="!compact" class="placeholder">Search AI tools...</span>
    <span v-if="!compact" class="kbd">{{ isMac ? '⌘' : 'Ctrl' }}K</span>
  </button>
</template>

<script setup lang="ts">
defineProps<{
  expanded?: boolean
  compact?: boolean
}>()

const isMac = computed(() => {
  if (import.meta.client) {
    return navigator.platform.includes('Mac')
  }
  return true
})

function openSearchModal() {
  const { open } = useSearch()
  open()
}
</script>

<style scoped>
button { font: inherit; text-align: left; }
button:focus-visible {
  outline: 2px solid var(--color-text-primary);
  outline-offset: 3px;
}
</style>
