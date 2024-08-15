<script setup>
import { useRouter } from "vue-router";
const router = useRouter();



function logoutFunc() {
  localStorage.removeItem("accessToken");
  router.push("/");
}
</script>

<template>
  <div>home page</div>
  <UButton @click="logoutFunc()" color="primary" variant="solid"
    >Button</UButton
  >
</template>
