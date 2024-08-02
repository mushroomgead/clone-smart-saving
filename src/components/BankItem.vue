<script setup lang="ts">
import { computed, ref } from 'vue'

const props = defineProps<{
  name: string
  logo?: string
  interest: number
  bank?: string
  totalInterest?: number
  saving: number
}>()

const interestPercentage = computed(() => Number(props.interest * 100).toFixed(2))
const totalInterestPercentage = computed(() =>
  props.totalInterest ? props.totalInterest.toFixed(2) : 0.0
)
const saveAmountFormat = computed(() => props.saving.toFixed(2))
</script>

<template>
  <div class="border-2 flex justify-between p-2 my-2 rounded-md min-h-[60px]">
    <div class="flex">
      <img v-show="logo" :src="logo" class="rounded-md w-12 h-12" />
      <div class="ml-3 flex flex-col justify-center">
        <div>
          <span class="font-bold text-sm mr-2">{{ name }}</span>
          <span class="bg-green-300 rounded-lg text-xs px-1">{{ interestPercentage }}%</span>
        </div>
        <div v-show="bank" class="text-xs text-gray-400">{{ bank }}</div>
      </div>
    </div>

    <div class="flex flex-col items-end justify-center">
      <div class="font-bold text-sm">฿{{ saveAmountFormat }}</div>
      <div v-show="totalInterest" class="text-xs text-gray-400">
        <span class="mr-1">ดอกเบี้ย</span>฿{{ totalInterestPercentage }}
      </div>
    </div>
  </div>
</template>
