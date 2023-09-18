<template>
  <button
    :class="outline"
    class="border border-pink-700 px-5 py-1 font-semibold transition-all delay-75 flex space-x-2 items-center"
  >
    <Icon
      v-if="props.icon != undefined"
      :name="props.icon"
      color="red"
      size="18px"
    />
    <span v-if="props.label != undefined" class="text-inherit">
      {{ props.label }}
    </span>
  </button>
</template>

<script lang="ts" setup>
const props = defineProps(["label", "outline", "icon", "flat", "rounded"]);

const outline = computed(() => {
  return [
    props.outline != undefined
      ? "hover:bg-pink-700/10 !text-pink-700"
      : "bg-pink-700",
    props.rounded != undefined ? "rounded-full" : "rounded-md",
    props.flat != undefined
      ? "hover:bg-pink-700/10 text-pink-700 bg-transparent border-none"
      : "text-white",
  ];
});
</script>

<style>
</style>
