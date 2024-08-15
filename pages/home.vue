<script setup>
import { useRouter } from "vue-router";
import { onMounted } from "vue";
const router = useRouter();

onMounted(() => {
  if (typeof window !== "undefined") {
    const token = localStorage.getItem("accessToken");

    if (token.includes("eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.ey")) {
      // Agar token mavjud bo'lsa, home sahifada qoladi yoki boshqa sahifaga yo'naltiradi
      router.push("/home");
    } else {
      // Agar token mavjud bo'lmasa, login sahifasiga yo'naltiradi
      router.push("/");
    }
  }
});

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
