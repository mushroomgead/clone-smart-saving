<script setup lang="ts">
import BankItem from './BankItem.vue'
defineProps<{
  name: string
  logo: string
  interest: number
  bank: string
  totalInterest: number
  saving: number
}>()
</script>

<template>
  <BankItem
    :name="name"
    :logo="logo"
    :interest="interest"
    :bank="bank"
    :totalInterest="totalInterest"
    :saving="saving"
  />
</template>
