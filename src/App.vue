<script setup lang="ts">
import { ref } from "vue"
import Button from "@/components/Button.vue"
import FormInput from "@/components/FormInput.vue"
import FormField from "@/components/FormField/FormField.vue"

interface Fields {
  name: string
  email: string
  password: string
}

const form = ref<Fields>({
  name: "",
  email: "",
  password: "",
})

const errors = ref<Fields>({ name: "", email: "", password: "" })

function submit() {
  errors.value = {
    name: "Name is invalid because...",
    email: "Email is invalid because...",
    password: "Password is invalid because...",
  }
}
</script>

<template>
  <form
    class="mx-auto w-full max-w-md space-y-4 p-4"
    @submit.prevent="submit"
  >
    <FormField
      label="Name"
      required
      :error="errors.name"
    >
      <FormInput
        v-model="form.name"
        placeholder="John Doe"
        type="text"
      />
    </FormField>

    <FormField
      label="Email"
      required
      :error="errors.email"
    >
      <FormInput
        v-model="form.email"
        placeholder="john@doe.com"
        type="email"
      />
    </FormField>

    <FormField
      label="Password"
      required
      :error="errors.password"
      help="Sould be at least 8 characters long."
    >
      <FormInput
        v-model="form.password"
        type="password"
      />
    </FormField>

    <div class="flex justify-end">
      <Button intent="primary">Register</Button>
    </div>
  </form>
</template>
