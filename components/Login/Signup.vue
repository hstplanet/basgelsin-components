<template>
  <div class="bg-white shadow-md p-5 rounded-md w-[60%] h-[500px]">
    <div class="steper flex gap-3 flex-row" v-if="stepCount < 6">
      <div class="flex-1 h-[3px] rounded-full" v-for="i in isCompany != undefined ? 5 : 4" :key="i" :class="stepCount >= i ? 'bg-pink-700' : 'bg-gray-300'"></div>
    </div>
    <div class="h-full pt-5">
      <!-- Kişisel Bilgiler -->
      <div class="flex h-fit flex-row" v-if="stepCount == 1">
        <div class="flex items-center shrink">
          <img src="~/assets/images/auth-mail.png" class="h-[400px]" alt="" srcset="" />
        </div>
        <div class="text-gray-700 grow">
          <p class="text-2xl">Kullanıcı Bilgileri</p>
          <span class="">Lütfen kullanıcı bilgilerinizi tanımlayınız.</span>

          <div class="flex flex-col mt-5 gap-3">
            <Input v-model="createData.name" placeholder="Ad Soyad" icon="ic:baseline-account-circle" />
            <Input v-model="createData.emailAddress" placeholder="Email Adresi" icon="ic:baseline-attach-email" />
            <Input v-model="createData.phone" placeholder="Telefon" icon="ic:baseline-local-phone" />
            <span class="text-red-700" v-if="error.length > 0">{{ error }}</span>
          </div>
        </div>
      </div>

      <!-- Şifre -->
      <div class="flex h-fit flex-row" v-if="stepCount == 2">
        <div class="flex items-center shrink">
          <img src="~/assets/images/auth-password.png" class="h-[400px]" alt="" srcset="" />
        </div>
        <div class="text-gray-700 grow">
          <p class="text-2xl">Şifre Bilgileri</p>
          <span class="">Lütfen hesabınıza erişmek için şifre bilgilerinizi girin.</span>

          <div class="flex flex-col mt-5 gap-3">
            <Input v-model="createData.password" type="password" placeholder="Şifre" icon="ic:baseline-password" />
            <Input v-model="createData.repassword" type="password" placeholder="Şifre Tekrar" icon="ic:baseline-password" />
            <span class="text-red-700" v-if="error.length > 0">{{ error }}</span>
          </div>
        </div>
      </div>

      <!-- Photo -->
      <div class="flex h-fit flex-row" v-if="stepCount == 3">
        <div class="flex items-center shrink">
          <div class="w-[480px] h-[400px] flex flex-row items-center justify-center">
            <img src="~/assets/images/auth-default-user.jpg" class="h-44 rounded-full" alt="" srcset="" v-if="fileURL.length == 0" />
            <img :src="fileURL" class="h-44 rounded-full" alt="" srcset="" v-else />
          </div>
        </div>
        <div class="text-gray-700 grow">
          <p class="text-2xl">Profil Fotoğrafı</p>
          <span class="">Hesabınızı kişiselleştirin. Profile fotoğrafınızı şimdi yüklemeden devam edebilirsiniz.</span>

          <div class="flex flex-col mt-5 gap-3">
            <input @change="selectImage" type="file" name="" id="" />
          </div>
        </div>
      </div>

      <!-- Address -->
      <div class="flex h-fit flex-row" v-if="stepCount == 4">
        <div class="flex items-center shrink">
          <img src="~/assets/images/auth-address.png" class="h-[400px]" alt="" srcset="" />
        </div>
        <div class="text-gray-700 grow">
          <p class="text-2xl">Adres Bilgileri</p>
          <span class="">Adres bilgilerinizi doldurun.</span>

          <div class="flex flex-col mt-5 gap-3">
            <Input v-model="createData.address.name" type="text" placeholder="Adres Adı" icon="fluent-emoji-high-contrast:globe-showing-americas" />

            <select
              @input="selectCity"
              id="countries"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            >
              <option v-for="item in data" :key="item.plaka_kodu" :value="JSON.stringify(item)">{{ item.il_adi }}</option>
            </select>

            <select
              v-model="createData.address.town"
              id="countries"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            >
              <option :selected="index == 0" v-for="(item, index) in ilceler" :key="item.ilce_kodu" :value="item.ilce_adi">{{ item.ilce_adi }}</option>
            </select>

            <Input v-model="createData.address.fullAddress" type="textarea" placeholder="Açık Adres" icon="fluent-emoji-high-contrast:globe-showing-americas" />
            <span class="text-red-700" v-if="error.length > 0">{{ error }}</span>
          </div>
        </div>
      </div>

      <!-- Company -->
      <div class="flex h-fit flex-row" v-if="stepCount == 5">
        <div class="flex items-center shrink">
          <img src="~/assets/images/auth-company.png" class="h-[400px]" alt="" srcset="" />
        </div>
        <div class="text-gray-700 grow">
          <p class="text-2xl">Şirket Bilgileri</p>
          <span class="">Lütfen hesabınızı şirket olarak oluşturabilmemiz için bilgilerinizi giriniz.</span>

          <div class="flex flex-col mt-5 gap-3">
            <Input v-model="createData.name" type="text" placeholder="Firma Adı" icon="ic:baseline-password" />
            <Input v-model="createData.taxNumber" type="text" placeholder="Vergi No" icon="ic:baseline-password" />
            <Input v-model="createData.taxOffice" type="text" placeholder="Vergi Dairesi" icon="ic:baseline-password" />
            <Input v-model="createData.mersisNumber" type="text" placeholder="Mersis No" icon="ic:baseline-password" />
            <span class="text-red-700" v-if="error.length > 0">{{ error }}</span>
          </div>
        </div>
      </div>

      <!-- Finish -->
      <div class="flex h-full flex-row" v-if="stepCount == 6">
        <div class="text-gray-700 grow text-center h-full items-center flex flex-col justify-center">
          <img src="~/assets/logo/Logo-Pink.svg" class="h-16 mb-10" alt="" />
          <p class="text-2xl">Hesabınızı oluştururken lütfen bekleyin.</p>
          <span class="">Hesabınızı oluşturuyoruz. Bu işlem çok kısa sürecek. Hesabınız ile tüm ortak işletmelerimizden sipariş verebilirsiniz.</span>
        </div>
      </div>

      <div class="flex flex-row justify-end gap-4" v-if="stepCount < 6">
        <ButtonsBS label="Geri" @click="backStep" v-if="stepCount > 1" />
        <ButtonsBS :label="stepCount > (isCompany != undefined ? 4 : 3) ? 'Hesabımı Oluştur' : 'Devam Et'" @click="nextStep" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { data } from "~/assets/data/il-ilce.json"

const props = defineProps(["isCompany"])

const ilceler = ref<[{ ilce_adi: string; ilce_kodu: string }]>()

const stepCount = ref(1)
const fileURL = ref("")
const file = ref<File>()
const error = ref("")

const { createData, createUser } = useAccount()
const { validateEmail } = useValitade()
const { uploadFile } = useFile()

onMounted(() => {
  //@ts-ignore
  ilceler.value = data[0].ilceler
})

const nextStep = () => {
  if (stepCount.value == 1) {
    if (createData.value.name.length > 0 && createData.value.emailAddress.length > 0 && createData.value.phone.length > 0) {
      const validate = validateEmail(createData.value.emailAddress)
      if (validate.errorValue.value.length == 0) {
        stepCount.value += 1
      } else {
        errorMessage(validate.errorValue.value)
      }
    } else {
      emptyError()
    }
  } else if (stepCount.value == 2) {
    if (createData.value.password.length > 0 && createData.value.repassword.length > 0) {
      if (createData.value.password == createData.value.repassword) {
        stepCount.value += 1
      } else {
        errorMessage("Girdiğiniz şifrele uyuşmuyor.")
      }
    } else {
      emptyError()
    }
  } else if (stepCount.value == 3) {
    stepCount.value += 1
  } else if (stepCount.value == 4) {
    if (createData.value.address.name.length > 0 && createData.value.address.fullAddress.length > 0) {
      stepCount.value += props.isCompany != undefined ? 1 : 2
    } else {
      emptyError()
    }
  } else if (stepCount.value == 5) {
    if (createData.value.taxOffice.length > 0 && createData.value.taxNumber.length > 0 && createData.value.name.length > 0 && createData.value.mersisNumber.length > 0) {
      stepCount.value += 1
    } else {
      emptyError()
    }
  }

  if (stepCount.value == 6) {
    createUser()
  }
}

const emptyError = () => {
  error.value = "Lütfen tüm bilgileri doldurun"
  setTimeout(() => {
    error.value = ""
  }, 3000)
}

const errorMessage = (message: string) => {
  error.value = message
  setTimeout(() => {
    error.value = ""
  }, 3000)
}

const backStep = () => {
  stepCount.value -= 1
}

const selectImage = async (evt: Event) => {
  //@ts-ignore
  file.value = evt.target.files[0]
  const reader = new FileReader()
  reader.addEventListener(
    "load",
    () => {
      //@ts-ignore
      fileURL.value = reader.result
    },
    false
  )
  if (file.value) {
    reader.readAsDataURL(file.value)
  }

  const { data } = await uploadFile(file.value)
  //@ts-ignore
  createData.value.logo = data.value
  console.log(data.value)
}

const selectCity = (evt: any) => {
  ilceler.value = JSON.parse(evt.target.value).ilceler
  createData.value.address.city = JSON.parse(evt.target.value).il_adi
}
</script>



<style>
</style>
