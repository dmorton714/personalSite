<script setup>
defineProps({
  modelValue: {
    type: String,
    required: true
  },
  options: {
    type: Array,
    required: true
  },
  label: {
    type: String,
    default: 'Filter by:'
  }
})

defineEmits(['update:modelValue'])
</script>

<template>
  <div class="filter-bar no-print">
    <p v-if="label" class="filter-label">{{ label }}</p>
    
    <div class="filter-layout">
      <div class="button-group">
        <button
          v-for="option in options"
          :key="option"
          :class="{ active: modelValue === option }"
          @click="$emit('update:modelValue', option)"
        >
          {{ option }}
        </button>
      </div>

      <div class="actions-slot">
        <slot name="actions"></slot>
      </div>
    </div>
  </div>
</template>

<style scoped>
.filter-bar {
  margin-bottom: 2rem;
  text-align: center;
}

.filter-label {
  font-size: 0.8rem;
  color: #64748b;
  margin-bottom: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-weight: 600;
}

.filter-layout {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.button-group {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  flex-wrap: wrap;
}

button {
  background: #ffffff;
  border: 1px solid #e2e8f0;
  padding: 6px 14px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.875rem;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  color: #475569;
}

button:hover {
  background: #f8fafc;
  border-color: #cbd5e1;
}

button.active {
  background: #2563eb;
  color: white;
  border-color: #2563eb;
  box-shadow: 0 4px 6px -1px rgba(37, 99, 235, 0.2);
}

.actions-slot {
  display: flex;
  justify-content: center;
}

@media print {
  .no-print {
    display: none !important;
  }
}
</style>