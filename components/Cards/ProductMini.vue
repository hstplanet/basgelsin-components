<template>
  <div class="bg-white w-[280px] rounded-md shadow-md">
    <div class="w-full h-40 relative overflow-hidden">
      <div class="absolute left-0 top-2 py-2 z-10 flex flex-col gap-2">
        <span class="bg-pink-700 text-white py-1 px-2 rounded-tr-md rounded-br-md text-sm">Öne Cıkan</span>
        <span class="bg-pink-700 text-white py-1 px-2 rounded-tr-md rounded-br-md text-sm uppercase">%20 Indirim</span>
      </div>
      <img class="h-full w-full object-cover transform hover:scale-125 transition-all duration-500" src="https://images.deliveryhero.io/image/fd-tr/LH/tq3e-listing.jpg" alt="" />
    </div>
    <div class="p-2 text-gray-700">
      <!--  -->
      <div class="flex justify-between">
        <span class="font-serif">SR Döner</span>
        <div class="flex items-center gap-1">
          <Icon name="fontisto:star" color="red" size="16px" />
          <span class="text-sm">
            <span class="text-black font-medium">4.5/5</span>
            (5000+)
          </span>
        </div>
      </div>
      <!--  -->
      <div class="">
        <span class="font-serif text-ellipsis whitespace-nowrap overflow-hidden block text-sm text-gray-500">Döner Kebap & Türk Mutfağı Restoran Teslimatlı</span>
      </div>
      <!--  -->
      <div class="mt-5">
        <span class="font-semibold text-md text-gray-500">
          15 TL
          <span class="font-normal">minimum</span>
        </span>
      </div>
      <!--  -->
      <div class="">
        <span class="font-semibold text-md text-green-700">Ücretsiz Gönderim</span>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
</script>



<style>
</style>
