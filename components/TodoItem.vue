<template>
  <div
      :class="{ 'opacity-75': modelValue.completed }"
      class="flex flex-row items-start gap-4 rounded-lg p-4
               bg-gradient-to-b from-slate-900 to-slate-950
               border border-slate-800 hover:border-slate-700
               transition-all duration-300 group"
  >
    <!-- Checkbox -->
    <button
        :class="{ 'bg-cyan-400 border-cyan-400': modelValue.completed }"
        class="flex-shrink-0 w-5 h-5 mt-1 rounded border-2 border-slate-700
                   transition-colors duration-300 hover:border-cyan-400
                   flex items-center justify-center"
        @click="$emit('toggle')"
    >
      <svg
          v-if="modelValue.completed"
          class="h-3 w-3 text-slate-900"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
      >
        <path
            clip-rule="evenodd"
            d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
            fill-rule="evenodd"
        />
      </svg>
    </button>

    <!-- Task Text -->
    <div class="flex-1">
      <p
          :class="{ 'line-through text-slate-500': modelValue.completed }"
          class="text-slate-300 transition-all duration-300"
      >
        {{ modelValue.text }}
      </p>
      <p
          v-if="modelValue.completedAt"
          class="text-xs text-slate-500 mt-1"
      >
        Completed {{ formatTime(modelValue.completedAt) }}
      </p>
    </div>

    <!-- Delete Button -->
    <button
        aria-label="Delete task"
        class="text-slate-500 hover:text-red-400 transition-colors duration-300 p-1"
        @click="$emit('remove')"
    >
      <svg
          class="h-5 w-5"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
      >
        <path
            clip-rule="evenodd"
            d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
            fill-rule="evenodd"
        />
      </svg>
    </button>
  </div>
</template>

<script setup lang="ts">
interface TodoItem {
  text: string;
  completed: boolean;
  completedAt?: Date;
}

defineProps<{
  modelValue: TodoItem;
}>();

defineEmits<{
  (e: 'remove'): void;
  (e: 'toggle'): void;
}>();

function formatTime(date: Date): string {
  const now = new Date();
  const diff = Math.floor((now.getTime() - new Date(date).getTime()) / 1000);

  if (diff < 60) return 'just now';
  if (diff < 3600) return `${Math.floor(diff / 60)}m ago`;
  if (diff < 86400) return `${Math.floor(diff / 3600)}h ago`;
  return `${Math.floor(diff / 86400)}d ago`;
}
</script>