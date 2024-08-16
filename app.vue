<template>
  <div class="flex justify-center h-screen items-center">
    <NuxtPage />
  </div>
  <UNotifications />
</template>

<script setup>
import { onMounted } from "vue";
import { useRouter } from "vue-router";
const router = useRouter();

onMounted(() => {
  const token = localStorage.getItem("accessToken");

  if (token?.includes("eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.ey")) {
    // Agar token mavjud bo'lsa, home sahifada qoladi yoki boshqa sahifaga yo'naltiradi
    router.push("/home");
  } else {
    // Agar token mavjud bo'lmasa, login sahifasiga yo'naltiradi
    router.push("/");
  }
});
</script>
