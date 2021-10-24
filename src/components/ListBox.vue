<script setup>
import {
  Listbox,
  ListboxButton,
  ListboxOptions,
  ListboxOption
} from "@headlessui/vue";

const props = defineProps({
  options: Array,
  modelValue: Object,
});
</script>

<template>
  <div class="w-56 relative">
    <Listbox v-slot="{ open }" v-model="modelValue" @update:model-value="$emit('update:modelValue', $event)">
      <ListboxButton
        class="relative w-full py-2 pl-3 pr-10 cursor-default bg-gray-200 rounded-t-lg text-left focus:outline-none focus:ring-1 focus:ring-purple-200"
        :class="open ? 'rounded-b-none' : 'rounded-b-lg'"
      >
        <span>{{ modelValue.text }}</span>
        <span class="absolute inset-y-0 right-0 flex items-center pr-2 text-gray-400">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
          </svg>
        </span>
      </ListboxButton>
      <transition
        leave-active-class="transition duration-100 ease-in"
        leave-from-class="opacity-100"
        leave-to-class="opacity-0"
        enter-active-class="transition duration-100 ease-in"
        enter-from-class="opacity-0"
        enter-to-class="opacity-100"
      >
        <ListboxOptions class="absolute w-full py-1 overflow-auto bg-gray-100 rounded-b-lg max-h-60 focus:outline-none">
          <ListboxOption
            v-slot="{ active, selected }"
            v-for="Option in options"
            :key="Option"
            :value="Option"
            as="template"
          >
            <li
              class="relative cursor-default py-2 pl-10 pr-4"
              :class="active || selected ? 'bg-purple-100' : 'text-gray-900'"
            >
              <span>{{ Option.text }}</span>
              <span
                v-if="selected"
                class="absolute inset-y-0 left-0 flex items-center pl-3"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
              </span>
            </li>
          </ListboxOption>
        </ListboxOptions>
      </transition>
    </Listbox>
  </div>
</template>

<style>

</style>
