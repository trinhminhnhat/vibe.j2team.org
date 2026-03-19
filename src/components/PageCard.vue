<script setup lang="ts">
import { RouterLink } from 'vue-router'
import type { PageInfo } from '@/types/page'
import FavoriteButton from '@/components/FavoriteButton.vue'

defineProps<{
  page: PageInfo
  /** Always show the favorite button (e.g. on bookmarks page). Default: show on hover only. */
  alwaysVisibleFavorite?: boolean
  /** Use compact sizing for horizontal scroll layouts */
  compact?: boolean
}>()
</script>

<template>
  <RouterLink
    :to="page.path"
    class="group relative flex flex-col border border-border-default bg-bg-surface transition-all duration-300 hover:-translate-y-1 hover:border-l-4 hover:border-l-accent-coral hover:bg-bg-elevated hover:shadow-lg hover:shadow-accent-coral/5"
    :class="compact ? 'p-4' : 'p-6'"
  >
    <FavoriteButton
      :path="page.path"
      :class="compact ? 'top-2 right-2' : 'top-3 right-4'"
      :always-visible="alwaysVisibleFavorite"
    />

    <slot name="background" />

    <h3
      class="font-display font-semibold text-text-primary group-hover:text-accent-coral transition-colors"
      :class="compact ? 'text-sm line-clamp-1' : 'text-lg'"
    >
      {{ page.name }}
    </h3>
    <p
      class="text-text-secondary line-clamp-2"
      :class="compact ? 'mt-1.5 text-xs' : 'mt-2 text-sm'"
      :title="page.description"
    >
      {{ page.description }}
    </p>
    <p
      class="mt-auto text-text-dim font-display tracking-wide"
      :class="compact ? 'pt-3 text-[10px]' : 'pt-4 text-xs'"
    >
      bởi
      <a
        v-if="page.facebook"
        :href="page.facebook"
        target="_blank"
        rel="noopener noreferrer"
        class="text-accent-coral hover:underline"
        @click.stop
      >
        {{ page.author }}
      </a>
      <span v-else>{{ page.author }}</span>
    </p>
  </RouterLink>
</template>
