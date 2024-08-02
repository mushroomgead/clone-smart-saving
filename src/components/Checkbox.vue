<script setup lang="ts">
defineProps<{
  isChecked: boolean
}>()
</script>
<template>
  <div class="mt-2">
    <input
      type="checkbox"
      id="canSavingMore2Years"
      class="mr-2"
      :checked="isChecked"
      @click="$emit('toggleSavingMore2Years')"
    />
    <label for="canSavingMore2Years">สามารถฝากเงินได้เกิน 2 ปี</label>
  </div>
</template>
