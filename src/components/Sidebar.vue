<template>
  <aside
    :class="[
      'sticky top-0 h-screen bg-white dark:bg-gray-900 border-r border-gray-200 dark:border-gray-700 transition-all duration-300 ease-in-out overflow-hidden flex-shrink-0',
      isCollapsed ? 'w-16' : 'w-64',
    ]"
  >
    <!-- Sidebar Header -->
    <div
      class="flex items-center justify-between h-16 px-4 border-b border-gray-200 dark:border-gray-700"
    >
      <div
        :class="[
          'flex items-center gap-2 transition-opacity duration-200 min-w-0',
          isCollapsed ? 'opacity-0 w-0 overflow-hidden' : 'opacity-100',
        ]"
      >
        <div class="text-2xl flex-shrink-0">🎨</div>
        <span
          class="font-semibold text-gray-900 dark:text-gray-100 whitespace-nowrap"
          >Tailwind UI</span
        >
      </div>
      <button
        @click="toggleSidebar"
        class="p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 text-gray-600 dark:text-gray-400 transition-colors duration-200 flex-shrink-0"
        :title="isCollapsed ? 'Expand sidebar' : 'Collapse sidebar'"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="20"
          height="20"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          :class="[
            'transition-transform duration-200',
            isCollapsed ? 'rotate-180' : '',
          ]"
        >
          <path d="m15 18-6-6 6-6" />
        </svg>
      </button>
    </div>

    <!-- Sidebar Content -->
    <nav
      class="flex flex-col h-[calc(100vh-4rem)] overflow-y-auto overflow-x-hidden py-4"
    >
      <!-- Navigation Items -->
      <div class="flex-1 px-3 space-y-1">
        <SidebarItem
          v-for="item in navigationItems"
          :key="item.id"
          :item="item"
          :isCollapsed="isCollapsed"
          :isActive="activeItem === item.id"
          :activeChildId="activeChildItem"
          @click="setActiveItem(item.id)"
          @childClick="handleChildClick"
        />
      </div>

      <!-- Sidebar Footer -->
      <div class="px-3 pt-4 mt-4 border-t border-gray-200 dark:border-gray-700">
        <SidebarItem
          :item="settingsItem"
          :isCollapsed="isCollapsed"
          :isActive="activeItem === 'settings'"
          @click="setActiveItem('settings')"
        />
      </div>
    </nav>
  </aside>
</template>

<script setup lang="ts">
import { ref } from "vue";
import SidebarItem from "./SidebarItem.vue";

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

const isCollapsed = ref(false);
const activeItem = ref("models");
const activeChildItem = ref("genesis");

const navigationItems: NavigationItem[] = [
  {
    id: "models",
    label: "Models",
    icon: "📦",
    children: [
      { id: "genesis", label: "Genesis" },
      { id: "explorer", label: "Explorer" },
      { id: "quantum", label: "Quantum" },
    ],
  },
  { id: "colors", label: "Color Schemes", icon: "🎨" },
  { id: "layouts", label: "Responsive Layouts", icon: "📐" },
  {
    id: "components",
    label: "Interactive Components",
    icon: "🧩",
    children: [
      { id: "buttons", label: "Buttons", badge: "New" },
      { id: "cards", label: "Cards" },
      { id: "modals", label: "Modals" },
    ],
  },
  { id: "forms", label: "Form Elements", icon: "📝" },
  { id: "animations", label: "Animations", icon: "✨" },
  { id: "typography", label: "Typography", icon: "📄" },
];

const settingsItem: NavigationItem = {
  id: "settings",
  label: "Settings",
  icon: "⚙️",
};

function toggleSidebar() {
  isCollapsed.value = !isCollapsed.value;
}

function setActiveItem(itemId: string) {
  activeItem.value = itemId;
  activeChildItem.value = "";
  // Handle navigation here
}

function handleChildClick(child: ChildItem) {
  activeChildItem.value = child.id;
  // Handle child navigation here
  console.log("Child clicked:", child);
}

// Expose methods and state for parent components
defineExpose({
  isCollapsed,
  toggleSidebar,
  setActiveItem,
});
</script>

<style scoped>
/* Custom scrollbar for sidebar */
nav::-webkit-scrollbar {
  width: 6px;
}

nav::-webkit-scrollbar-track {
  background: transparent;
}

nav::-webkit-scrollbar-thumb {
  background: rgba(156, 163, 175, 0.3);
  border-radius: 3px;
}

nav::-webkit-scrollbar-thumb:hover {
  background: rgba(156, 163, 175, 0.5);
}
</style>
