<script setup lang="ts">
import BankList from './components/BankList.vue'
import Checkbox from './components/Checkbox.vue'
import Result from './components/Result.vue'
import TextInput from './components/TextInput.vue'
</script>

<template>
  <div>
    <header>
      <div class="bg-rose-800 h-60 w-full">
        <div class="flex flex-col justify-center items-center text-white pt-14">
          <h1 class="text-bold">ฝากเงินที่ไหนดี ?</h1>
          <h4>version clone..</h4>
        </div>
      </div>
    </header>

    <main class="container mx-auto relative top-[-70px] center">
      <div class="border-2 p-4 rounded-lg bg-white">
        <div v-show="false">
          <TextInput />
          <Checkbox />
          <button class="w-full bg-rose-800 p-2 rounded-md text-white mt-2">คำนวณ</button>
        </div>
        <Result />
      </div>

      <BankList />
    </main>
    <footer class="bg-rose-800 h-24 w-full absolute bottom-0"></footer>
  </div>
</template>
