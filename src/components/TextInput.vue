<script setup lang="ts">
const emit = defineEmits(['onMoneyChange'])

function handleOnChange(event: any) {
  emit('onMoneyChange', event.target.value)
}
</script>

<template>
  <div>
    <label for="moneyInput">จำนวนเงินออม (บาท)</label>
    <input
      type="number"
      id="moneyInput"
      name="moneyInput"
      class="w-full border-2 rounded-md p-2"
      @input="handleOnChange"
    />
  </div>
</template>
