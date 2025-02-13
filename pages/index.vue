<template>
  <div class="min-h-full flex flex-col">
    <!-- Header Section -->
    <div class="flex items-center justify-between mb-8">
      <div>
        <h1 class="font-bold text-4xl bg-gradient-to-r from-slate-50 to-slate-300 bg-clip-text text-transparent">
          Tasks
        </h1>
        <p class="text-slate-400 mt-2">{{ taskCount }}</p>
      </div>

      <!-- Action Buttons -->
      <div class="flex gap-4">
        <button
            v-if="items.length > 0"
            class="text-sm text-slate-400 hover:text-slate-300 transition-colors flex items-center gap-2"
            @click="clearCompleted"
        >
          <svg class="h-4 w-4" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
            <path clip-rule="evenodd"
                  d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
                  fill-rule="evenodd"/>
          </svg>
          Clear completed
        </button>
      </div>
    </div>

    <!-- Tasks List -->
    <div class="flex-1 flex flex-col gap-4 min-h-[200px]">
      <TransitionGroup
          class="flex flex-col gap-4"
          name="list"
          tag="div"
      >
        <!-- Empty State -->
        <div
            v-if="items.length === 0"
            key="empty"
            class="flex-1 flex flex-col items-center justify-center text-center p-8"
        >
          <div class="w-16 h-16 mb-4 rounded-full bg-slate-800 flex items-center justify-center">
            <svg class="h-8 w-8 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"
                 xmlns="http://www.w3.org/2000/svg">
              <path
                  d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"
                  stroke-linecap="round" stroke-linejoin="round"
                  stroke-width="2"/>
            </svg>
          </div>
          <p class="text-slate-400 mb-2">No tasks yet</p>
          <p class="text-sm text-slate-500">Add your first task using the form below</p>
        </div>

        <!-- Task Items -->
        <TodoItem
            v-for="(item, index) in items"
            :key="index"
            :model-value="item"
            @remove="removeItem(index)"
            @toggle="toggleItem(index)"
        />
      </TransitionGroup>
    </div>

    <!-- Add Task Form -->
    <form
        class="sticky bottom-0 pt-4 pb-10 bg-gradient-to-t from-slate-950 via-slate-950/95 to-transparent"
        @submit.prevent="addItem"
    >
      <div class="flex gap-4">
        <input
            v-model="text"
            :disabled="isAdding"
            class="flex-1 border border-slate-700 text-sm rounded-xl px-4 py-2.5
                           bg-slate-900/50 backdrop-blur placeholder:text-slate-500
                           focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-cyan-400
                           focus-visible:border-transparent transition-all duration-300"
            placeholder="Add a new task..."
            required
            type="text"
            @keydown.esc="text = ''"
        />
        <button
            :disabled="isAdding || !text.trim()"
            class="flex items-center gap-2 px-6 py-2.5 font-medium text-sm text-slate-900 bg-cyan-400
                           rounded-xl transition-all duration-300 hover:bg-cyan-300
                           hover:shadow-lg hover:shadow-cyan-400/25 active:scale-95
                           disabled:opacity-50 disabled:pointer-events-none"
            type="submit"
        >
          <svg
              v-if="isAdding"
              class="animate-spin h-4 w-4"
              fill="none"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
          >
            <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
            <path class="opacity-75"
                  d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
                  fill="currentColor"></path>
          </svg>
          <span>Add Task</span>
        </button>
      </div>
    </form>
  </div>
</template>

<script setup lang="ts">
// Types
interface TodoItem {
  text: string;
  completed: boolean;
  completedAt?: Date;
}

// State
const items = useState<TodoItem[]>("todos", () => []);
const text = ref("");
const isAdding = ref(false);

// Meta
useSeoMeta({
  title: 'Tasks',
  description: 'Manage your tasks efficiently',
});

// Computed
const taskCount = computed(() => {
  const total = items.value.length;
  const completed = items.value.filter(item => item.completed).length;
  if (total === 0) return 'No tasks';
  return `${completed}/${total} completed`;
});

// Methods
async function addItem() {
  const trimmedText = text.value.trim();
  if (!trimmedText) return;

  isAdding.value = true;
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 300));
    items.value.unshift({
      text: trimmedText,
      completed: false
    });
    text.value = "";
  } finally {
    isAdding.value = false;
  }
}

function removeItem(index: number) {
  items.value = items.value.filter((_, i) => i !== index);
}

function toggleItem(index: number) {
  const item = items.value[index];
  item.completed = !item.completed;

  if (item.completed) {
    item.completedAt = new Date();
  } else {
    delete item.completedAt;
  }
}

function clearCompleted() {
  items.value = items.value.filter(item => !item.completed);
}

// Page meta
definePageMeta({
  layout: "dashboard",
});

// Keyboard shortcuts
onMounted(() => {
  const handleKeyboard = (e: KeyboardEvent) => {
    // Ctrl/Cmd + Enter to add task
    if ((e.ctrlKey || e.metaKey) && e.key === 'Enter' && text.value.trim()) {
      addItem();
    }
  };

  window.addEventListener('keydown', handleKeyboard);
  onUnmounted(() => {
    window.removeEventListener('keydown', handleKeyboard);
  });
});
</script>

<style scoped>
/* List transitions */
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.3s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.list-leave-active {
  position: absolute;
}
</style>