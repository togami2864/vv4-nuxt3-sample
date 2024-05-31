<script setup lang="ts">
import type { RuleExpression } from 'vee-validate';
import { Field as VeeField} from 'vee-validate';

const props = defineProps<{
  name: string;
  label?: string;
  rules: RuleExpression<unknown>;
}>();
</script>

<template>
  <VeeField
    v-slot="{ errors, value, meta, validate }"
    :name="props.name"
    :label="props.label || props.name"
    :rules="props.rules"
  >
    <slot
      :errors="errors"
      :hasError="!meta.valid && errors.length > 0"
      :value="value"
      :meta="meta"
      :validate="validate"
    />
  </VeeField>
</template>
