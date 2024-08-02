<script setup lang="ts">
import { ref } from 'vue'
import BankList from './components/BankList.vue'
import Checkbox from './components/Checkbox.vue'
import Result from './components/Result.vue'
import TextInput from './components/TextInput.vue'
import BankItem from './components/BankItem.vue'
import { banksList } from '@/data/banks'
import type { Banks } from './types/banks'

const canSavingMore2Years = ref(true)
const shouldShowResult = ref(false)
let money = ref('')
let totalInterest = ref(0)
let totalSaving = ref(0)

let bankData = ref(banksList)

function toggleSaveMore2Years() {
  canSavingMore2Years.value = !canSavingMore2Years.value
}

function onCaculate() {
  bankData.value = filterBank(Number(money.value), canSavingMore2Years.value)
  totalSaving = bankData.value.reduce((accu: any, bank: any) => accu + bank.totalInterest, 0)
  totalInterest.value = Number(totalSaving) / Number(money.value)

  shouldShowResult.value = true
}

function filterBank(money: number, canSaveMore2Years: boolean) {
  let remaining = money
  let banks: Banks[] = []

  function deposit(amount: number, bank: string) {
    if (remaining <= 0) return
    const saveAmount = Math.min(remaining, amount)
    const initBank = banksList[bank]
    const totalInterest = initBank.interest * saveAmount
    const interest = initBank.interest
    banks.push({ ...initBank, interest, name: bank, saving: saveAmount, totalInterest })

    remaining -= saveAmount
  }

  deposit(10000, 'dime')
  deposit(10000, 'kkp')
  deposit(100000, 'chill-d')
  deposit(100000, 'me-save')
  deposit(40000, 'kkp2')
  deposit(500000, 'alpha')

  if (remaining >= 1000000) {
    deposit(1000000, 'lh-b-wealth')
  } else if (remaining > 0) {
    if (canSaveMore2Years) {
      deposit(remaining, 'kept')
    } else {
      if (remaining < 385000) {
        deposit(remaining, 'me-save2')
      } else {
        deposit(remaining, 'cimb')
      }
    }
  }

  return banks
}

function onReCaculate() {
  bankData.value = banksList
  shouldShowResult.value = false
}

function onMoneyChange(str: string) {
  money.value = str
}
</script>

<template>
  <div>
    <header>
      <div class="bg-rose-800 h-60 w-full">
        <div class="flex flex-col justify-center items-center text-white pt-14">
          <h1 class="font-bold">ฝากเงินที่ไหนดี ?</h1>
          <h4>clone from เนิร์ดไฟแนนซ์ x CodeTraveler..</h4>
        </div>
      </div>
    </header>

    <main class="container mx-auto relative top-[-70px] center">
      <div class="border-2 p-4 rounded-lg bg-white">
        <div v-show="!shouldShowResult">
          <TextInput :money="money" @on-money-change="onMoneyChange" />
          <Checkbox
            @toggle-saving-more2-years="toggleSaveMore2Years"
            :isChecked="canSavingMore2Years"
          />
          <button class="w-full bg-rose-800 p-2 rounded-md text-white mt-2" @click="onCaculate">
            คำนวณ
          </button>
        </div>
        <Result
          v-show="shouldShowResult"
          @re-caculate="onReCaculate"
          :canSavingMore2Years="canSavingMore2Years"
          :savingMoney="money"
        />
      </div>
      <div class="mt-4" v-show="shouldShowResult">
        <h3 class="font-bold">ดอกเบี้ยรวมโดยประมาณ (หากฝากเงิน 1 ปี)</h3>
        <BankItem name="ดอกเบี้ยรวมทุกธนาคาร" :interest="totalInterest" :saving="totalSaving" />
      </div>

      <div class="mt-4">
        <h3 class="font-bold">ฝากที่ไหนบ้าง</h3>
        <BankList
          v-for="bank in bankData"
          :name="bank.name"
          :logo="bank.logo"
          :interest="bank.interest"
          :bank="bank.bank"
          :totalInterest="bank.totalInterest"
          :saving="bank.saving || 0"
        />
      </div>
    </main>
    <footer class="bg-rose-800 h-24 w-full relative bottom-0"></footer>
  </div>
</template>
