<template>
  <div class="border border-gray-400/60 rounded-md p-2 flex flex-row justify-between items-center space-x-3">
    <input class="bg-transparent outline-none w-full" :type="type" :multiple="type == 'textarea'" v-model="value" :placeholder="placeholder" />
    <Icon v-if="icon != undefined" :name="icon" size="16px" color="gray" />
  </div>
</template>

<script lang="ts" setup>
const props = defineProps(["modelValue", "icon", "type", "placeholder"])
const emit = defineEmits(["update:modelValue"])

const value = computed({
  get() {
    return props.modelValue
  },
  set(value) {
    emit("update:modelValue", value)
  },
})
</script>



<style>
</style>
