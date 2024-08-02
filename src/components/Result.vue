<script setup lang="ts">
defineProps<{
  canSavingMore2Years: boolean
  savingMoney: string
}>()
</script>
<template>
  <div class="flex flex-col items-center">
    <div class="text-gray-500">จำนวนเงินออม</div>
    <h2 class="font-bold">฿{{ savingMoney }}</h2>

    <div class="mt-2">
      <span v-if="canSavingMore2Years">ฝากยาว มากกว่า 2 ปี</span>
      <span v-else>ฝากสั้น ไม่ถึง 2 ปี</span>
    </div>
    <button
      class="border-2 w-full text-rose-800 border-rose-800 rounded-lg p-2 mt-2"
      @click="$emit('re-caculate')"
    >
      คำนวณใหม่
    </button>
    <div class="bg-gray-100 text-xs text-gray-400 p-2 rounded-lg mt-4 w-full">
      <span class="font-bold text-gray-500">Disclaimer</span>
      ข้อมูลที่ได้จากการคำนวณเป็นเพียงการประมาณการเท่านั้น
    </div>
  </div>
</template>
