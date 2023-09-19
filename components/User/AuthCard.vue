<template>
  <div class="flex flex-row gap-3 p-2 hover:bg-slate-400/20 rounded-md" v-if="getUser">
    <img class="w-10 h-10 rounded-full" :src="getUser.profile.photoUrl" alt="" />
    <div class="flex-col flex justify-center leading-5 cursor-pointer">
      <span>{{getUser.fullName}}</span>
      <span class="text-gray-600">{{getUser.emailAddress}}</span>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { useUserStore } from "~/../basgelsin-server/stores/User"
import { storeToRefs } from "pinia"

const user = useUserStore()
const { getUser } = storeToRefs(user)



</script>



<style>
</style>
