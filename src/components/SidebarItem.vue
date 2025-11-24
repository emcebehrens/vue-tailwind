<template>
  <div>
    <button
      @click="handleClick"
      :class="[
        'w-full flex items-center gap-3 px-3 py-2 rounded-lg transition-all duration-200 group relative',
        isActive
          ? 'bg-blue-50 dark:bg-blue-950/30 text-blue-600 dark:text-blue-400'
          : 'text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-800',
      ]"
      :title="isCollapsed ? item.label : ''"
    >
      <!-- Icon -->
      <span class="text-xl flex-shrink-0">{{ item.icon }}</span>

      <!-- Label -->
      <span
        :class="[
          'text-sm font-medium whitespace-nowrap transition-opacity duration-200 overflow-hidden',
          isCollapsed ? 'opacity-0 w-0' : 'opacity-100 flex-1 text-left',
        ]"
      >
        {{ item.label }}
      </span>

      <!-- Badge -->
      <span
        v-if="item.badge && !isCollapsed"
        class="px-2 py-0.5 text-xs font-medium bg-blue-100 dark:bg-blue-900 text-blue-600 dark:text-blue-400 rounded-full flex-shrink-0"
      >
        {{ item.badge }}
      </span>

      <!-- Chevron for items with children -->
      <svg
        v-if="item.children && item.children.length > 0 && !isCollapsed"
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        :class="[
          'transition-transform duration-200 flex-shrink-0',
          isExpanded ? 'rotate-90' : '',
        ]"
      >
        <path d="m9 18 6-6-6-6" />
      </svg>

      <!-- Tooltip for collapsed state -->
      <div
        v-if="isCollapsed"
        class="absolute left-full ml-2 px-3 py-2 bg-gray-900 dark:bg-gray-700 text-white text-sm rounded-lg opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-200 whitespace-nowrap z-50 pointer-events-none"
      >
        {{ item.label }}
        <div
          class="absolute right-full top-1/2 -translate-y-1/2 border-4 border-transparent border-r-gray-900 dark:border-r-gray-700"
        ></div>
      </div>
    </button>

    <!-- Children (nested items) -->
    <div
      v-if="item.children && item.children.length > 0 && !isCollapsed"
      :class="[
        'overflow-hidden transition-all duration-200 ease-in-out',
        isExpanded ? 'max-h-96 opacity-100' : 'max-h-0 opacity-0',
      ]"
    >
      <div
        class="ml-6 mt-1 space-y-1 border-l-2 border-gray-200 dark:border-gray-700 pl-2"
      >
        <button
          v-for="child in item.children"
          :key="child.id"
          @click="handleChildClick(child)"
          :class="[
            'w-full flex items-center gap-2 px-3 py-1.5 rounded-lg text-sm transition-all duration-200',
            activeChildId === child.id
              ? 'bg-blue-50 dark:bg-blue-950/30 text-blue-600 dark:text-blue-400 font-medium'
              : 'text-gray-600 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 hover:text-gray-900 dark:hover:text-gray-200',
          ]"
        >
          <span class="text-left flex-1 overflow-hidden text-ellipsis">{{
            child.label
          }}</span>
          <span
            v-if="child.badge"
            class="ml-auto px-1.5 py-0.5 text-xs font-medium bg-blue-100 dark:bg-blue-900 text-blue-600 dark:text-blue-400 rounded-full flex-shrink-0"
          >
            {{ child.badge }}
          </span>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface ChildItem {
  id: string;
  label: string;
  badge?: string;
}

interface NavigationItem {
  id: string;
  label: string;
  icon: string;
  badge?: string;
  children?: ChildItem[];
}

interface Props {
  item: NavigationItem;
  isCollapsed: boolean;
  isActive: boolean;
  activeChildId?: string;
}

const props = defineProps<Props>();

const emit = defineEmits<{
  click: [];
  childClick: [child: ChildItem];
}>();

const isExpanded = ref(false);

function handleClick() {
  if (props.item.children && props.item.children.length > 0) {
    isExpanded.value = !isExpanded.value;
  } else {
    emit("click");
  }
}

function handleChildClick(child: ChildItem) {
  emit("childClick", child);
}
</script>
