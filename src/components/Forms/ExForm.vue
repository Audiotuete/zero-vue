<script setup lang="ts">
import { ref } from 'vue'
import Button from '@/components/Button.vue'
import FormFieldInput from '@/components/Forms/FormFieldInput.vue'
import FormField from '@/components/Forms/FormField.vue'

interface Fields {
  name: string
  email: string
  password: string
  notes: string
}

const form = ref<Fields>({
  name: '',
  email: '',
  password: '',
  notes: ''
})

const errors = ref<Fields>({ name: '', email: '', password: '', notes: '' })

function submit() {
  errors.value = {
    name: 'Name is invalid because...',
    email: 'Email is invalid because...',
    password: 'Password is invalid because...',
    notes: ''
  }
}
</script>

<template>
  <form @submit.prevent="submit">
    <FormField label="Name" required :error="errors.name">
      <FormFieldInput v-model="form.name" placeholder="John Doe" type="text" />
    </FormField>

    <FormField label="Email" required :error="errors.email">
      <FormFieldInput v-model="form.email" placeholder="john@doe.com" type="email" />
    </FormField>

    <FormField
      label="Password"
      required
      :error="errors.password"
      help="Sould be at least 8 characters long."
    >
      <FormFieldInput v-model="form.password" type="password" />
    </FormField>

    <FormField label="Notes">
      <FormFieldInput multiline v-model="form.notes" placeholder="Important notes" type text />
    </FormField>
    <div>
      <Button>Register</Button>
    </div>
  </form>
</template>
