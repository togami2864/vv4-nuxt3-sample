<script setup lang="ts">
import { ref } from 'vue';
import { Form as VeeForm } from 'vee-validate';

const $emit = defineEmits(['submit']);
const observer = ref<InstanceType<typeof VeeForm> | null>(null);

const onSubmit = () => {
  const observerRef = observer.value;
  if (!observerRef || !observerRef.getMeta().valid) {
    return;
  }
  const values = observerRef.getValues();
  $emit('submit', values);
};
</script>

<template>
  <VeeForm
    ref="observer"
    v-slot="{ errors, meta }"
    class="Form"
    @submit="onSubmit"
  >
    <slot :failed="!meta.valid && !!errors" />
  </VeeForm>
</template>

<style>
.Form {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
}
</style>