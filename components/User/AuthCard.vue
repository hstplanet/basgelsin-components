<template>
  <UDropdown :items="items" :ui="{ item: { disabled: 'cursor-text select-text' } }" :popper="{ placement: 'bottom-start' }">
    <div class="flex flex-row gap-3 p-2 hover:bg-slate-400/20 rounded-md items-center" v-if="getUser">
      <UAvatar src="https://avatars.githubusercontent.com/u/739984?v=4" />
      <div class="flex-col flex justify-center leading-5 cursor-pointer">
        <span>{{ getUser.fullName }}</span>
        <span class="text-gray-600">{{ getUser.emailAddress }}</span>
      </div>
    </div>
    <template #account="{ item }">
      <div class="text-left">
        <p>Basgelsin Puanı</p>
        <p class="truncate font-medium text-gray-900 dark:text-white">
          {{ item.label }}
        </p>
      </div>
    </template>
    <template #item="{ item }">
      <span class="truncate" @click="item.action()">{{ item.label }}</span>
      <UIcon :name="item.icon" class="flex-shrink-0 h-4 w-4 text-gray-400 dark:text-gray-500 ms-auto" />
    </template>
  </UDropdown>
</template>

<script lang="ts" setup>
import { useUserStore } from "~/../basgelsin-server/stores/User"
import { storeToRefs } from "pinia"

const user = useUserStore()
const { getUser } = storeToRefs(user)
const { signout } = useLogin()

const items = [
  [
    {
      label: "50 BP",
      slot: "account",
      disabled: true,
      action: () => {},
    },
  ],
  [
    {
      label: "Ayarlar",
      icon: "i-heroicons-cog-8-tooth",
      action: () => {},
    },
  ],
  [
    {
      label: "Hesabım",
      icon: "i-heroicons-book-open",
      action: () => {},
    },
    {
      label: "Favoriler",
      icon: "i-heroicons-megaphone",
      action: () => {},
    },
    {
      label: "Geçmiş Siparişler",
      icon: "i-heroicons-signal",
      action: () => {},
    },
  ],
  [
    {
      label: "Oturumu Kapat",
      icon: "i-heroicons-arrow-left-on-rectangle",
      action: () => {
        signout()
        const router = useRouter()
        router.push("/")
      },
    },
  ],
]
</script>



<style>
</style>
