<template>
  <div class="flex flex-col gap-3 mt-10">
    <Input v-model="email" type="text" icon="ic:outline-alternate-email" placeholder="Email Adresiniz" />
    <Input v-model="password" type="password" icon="ic:baseline-password" placeholder="Şifre" />
    <div class="flex justify-end cursor-pointer hover:text-pink-700">
      <NuxtLink to="/auth/reset">Şifremi Unuttum?</NuxtLink>
    </div>
    <ButtonsBS :loading="loading" @click="onLogin" label="Giriş Yap" class="w-full" />
    <ButtonsBS :loading="loading" to="/auth/signup" outline label="Kayıt Ol" class="w-full" />
  </div>
</template>

<script lang="ts" setup>
const { email, password, login } = useLogin()
const loading = ref(false)

const cookie = useCookie("basgelsin_auth")

const onLogin = async () => {
  const { data, pending, error, refresh } = await login()
  loading.value = pending.value

  if (!error.value) {
    //@ts-ignore
    cookie.value = data.value.signToken
    const rouuter = useRouter()
    rouuter.push("/")
  }
}

</script>



<style>
</style>
