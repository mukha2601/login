<script setup>
const toast = useToast();

// onMounted(() => {
//   toast.add({
//     id: "update_downloaded",
//     title: "Update downloaded.",
//     description: "It will be installed on restart. Restart now?",
//     icon: "i-octicon-desktop-download-24",
//     timeout: 3000,
//   });
// });

function onSubmit(event) {
  event.preventDefault();

  fetch("https://autoapi.dezinfeksiyatashkent.uz/api/auth/signin", {
    method: "POST",
    body: JSON.stringify({
      phone_number: state.phone,
      password: state.password,
    }),
    headers: {
      "Content-type": "application/json",
    },
  })
    .then((data) => data.json())
    .then((item) => {
      console.log(item);

      toast.add({
        id: "error",
        title: item.message,
        description: "It will be installed on restart. Restart now?",
        icon: "i-heroicons-check-circle",
        timeout: 2000,
      });

      
    })
    .catch((error) => {
      console.log("error");

      toast.add({
        title: error,
        icon: "material-symbols:cancel-outline",
        timeout: 3000,
        color:"red"
      });
    });
}

const state = reactive({
  phone: undefined,
  password: undefined,
});
</script>

<template>
  <div class="w-max p-8 border-2 border-primary">
    <UForm :state="state" class="space-y-4" @submit="onSubmit">
      <UFormGroup label="Phone" name="phone">
        <UInput v-model="state.phone" type="text" required minlength="3" />
      </UFormGroup>

      <UFormGroup label="Password" name="password">
        <UInput v-model="state.password" type="text" required minlength="3" />
      </UFormGroup>

      <UButton type="submit"> Submit </UButton>
    </UForm>
  </div>
</template>
