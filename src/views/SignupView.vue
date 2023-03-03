<script setup>
import UserForm from "@/components/UserForm.vue";

function signup(user) {
  // api request
}
</script>
<template>
  <div>
    <UserForm formType="signup" @submit="signup" />
    <!-- signup -->
  </div>
</template>
