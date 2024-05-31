<template>
  <div class="Layout">
    <ValidationObserver
      v-slot="{ failed }"
      @submit="onSubmit"
    >
      <ValidationProvider name="name" v-model="name" v-slot="{ errors, hasError }" rules="required" >
        <label for="name">Name</label>
        <input v-model="name" type="text" name="name" :class="{Error: hasError}"/>
        <span>{{ errors[0] }}</span>
      </ValidationProvider>
      <ValidationProvider name="email" v-model="email" v-slot="{ errors, hasError }" rules="required|email">
        <label for="email">Email</label>
        <input v-model="email" type="text" name="email" :class="{Error: hasError}"/>
        <span>{{ errors[0] }}</span>
      </ValidationProvider>
      <button type="submit" :disabled="failed">Submit</button>
    </ValidationObserver>
  </div>
</template>

<script lang="ts">
import ValidationObserver from './ValidationObserver.vue';
import ValidationProvider from './ValidationProvider.vue';
import {Field} from "vee-validate"

export default defineComponent({
  components: {
    ValidationProvider,
    ValidationObserver,
    Field,
  },
  data() {
    return {
      name: '',
      email: '',
    }
  },
  methods: {
    async onSubmit() {
      window.alert(`Form submitted => Name: ${this.name} Email: ${this.email}`)
    },
  },
})
</script>

<style>
.Layout {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.Error {
  border: 2px solid red;
}
</style>
