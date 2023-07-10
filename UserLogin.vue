<template>
  <section class="text-gray-600 body-font">
    <div class="mx-auto flex px-5">
      <div
        class="px-0 lg:px-10 xl:px-36 2xl:px-64 lg:pt-24 xl:pt-36 2xl:pt-64 mx-auto"
      >
        <div class="">
          <!-- <img
            src="@/assets/img/CM_Logo.svg"
            class="w-96 p-10 pb-2"
            alt="CourseMill Logo"
          /> -->
          <div class="w-96 p-10 pb-2.5">
            <div class="flex justify-center mb-2">
              <img
                :src="authLogo"
                alt="image is here"
                width="42"
                height="42"
                v-if="authLogo"
              />
              <logInSVG v-if="!authLogo" />
            </div>

            <h1
              class="text-3x text-blue-600 italic"
              style="font-size: 43px; font-family: 'Proxima Nova'"
            >
              <p v-if="authorName">{{ authorName }}</p>
              <p v-else class="flex justify-between">
                <span class="font-bold">RAPiD </span>
                <span class="font-normal">AUTHOR</span>
              </p>
            </h1>
          </div>

          <!-- toaster begin -->
          <div class="px-12 py-2" v-if="loginError">
            <div
              id="toast-success"
              class="flex items-center mx-auto p-1 border border-red-600 text-gray-500 bg-white rounded"
              role="alert"
            >
              <div
                class="inline-flex items-center justify-center flex-shrink-0 w-6 h-6 text-green-500 rounded-lg dark:bg-green-800 dark:text-green-200"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  class="fill-red-600"
                >
                  <path
                    d="M8 2.5a5.5 5.5 0 1 0 0 11 5.5 5.5 0 0 0 0-11Zm0 1a4.5 4.5 0 1 1 0 9 4.5 4.5 0 0 1 0-9Zm0 1.75a.75.75 0 1 0 0 1.5.75.75 0 0 0 0-1.5ZM8 7.5a.5.5 0 0 0-.5.5v2.5a.5.5 0 0 0 1 0V8a.5.5 0 0 0-.5-.5Z"
                  />
                </svg>
              </div>
              <div class="ml-3 text-sm font-normal text-red-600">
                {{ 'user-login.invalid-userid-or-password' }}
              </div>
              <button
                type="button"
                @click="loginError = false"
                class="ml-auto bg-white text-gray-400 hover:text-gray-900 rounded p-1.5 inline-flex h-6 w-6"
                data-dismiss-target="#toast-success"
                aria-label="Close"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  class="fill-red-600"
                >
                  <path
                    d="M3.378 3 3 3.378 7.622 8 3 12.622l.378.378L8 8.378 12.622 13l.378-.378L8.378 8 13 3.378 12.622 3 8 7.622 3.378 3Z"
                  />
                </svg>
              </button>
            </div>
          </div>

          <!-- toaster end -->

          <div class="w-96 px-10 py-6">
            <form class="space-y-6" @submit.prevent="">
              <div>
                <label
                  for="username"
                  class="block mb-2 text-sm font-normal text-gray-500"
                  >User ID</label
                >
                <input
                  type="text"
                  name="username"
                  id="username"
                  v-model="username"
                  class="bg-white border border-gray-300 text-gray-800 text-sm font-normal rounded focus:ring-primary-600 focus:border-primary-600 block w-full p-1"
                  placeholder=""
                  required
                />
              </div>
              <div>
                <label
                  for="password"
                  class="block mb-2 text-sm font-normal text-gray-500"
                  >Password</label
                >
                <div
                  class="flex flex-wrap w-full items-stretch bg-white border rounded border-gray-300"
                >
                  <input
                    v-if="!showPassword"
                    type="password"
                    name="password"
                    id="password"
                    v-model="password"
                    placeholder=""
                    class="flex-shrink flex-grow flex-auto bg-white border-0 border-gray-300 text-gray-800 font-normal text-sm rounded focus:ring-primary-600 focus:border-primary-600 block p-1"
                    required
                  />

                  <input
                    v-if="showPassword"
                    type="text"
                    name="password"
                    id="password"
                    v-model="password"
                    placeholder=""
                    class="flex-shrink flex-grow flex-auto bg-white border-0 border-gray-300 text-gray-800 font-normal text-sm rounded focus:ring-primary-600 focus:border-primary-600 block p-1"
                    required
                  />

                  <!-- eye or eye-slash icon -->
                  <div class="flex -mr-px">
                    <span
                      @click="showPassword = !showPassword"
                      class="flex items-center leading-normal bg-white rounded border-x px-3 pointer-events-auto text-gray-600"
                    >
                      <svg
                        v-if="!showPassword"
                        xmlns="http://www.w3.org/2000/svg"
                        width="16"
                        height="16"
                      >
                        <path
                          d="M8 3.5C4.375 3.5 1.25 6.518 1.25 8c0 1.482 3.125 4.5 6.75 4.5 3.626 0 6.75-3.018 6.75-4.5 0-1.482-3.124-4.5-6.75-4.5Zm0 1c3.236 0 5.75 2.792 5.75 3.5 0 .708-2.514 3.5-5.75 3.5S2.25 8.708 2.25 8c0-.708 2.514-3.5 5.75-3.5Zm0 .75a2.75 2.75 0 1 0 0 5.5 2.75 2.75 0 0 0 0-5.5ZM8 7a1 1 0 1 1 0 2 1 1 0 0 1 0-2Z"
                        />
                      </svg>

                      <svg
                        v-if="showPassword"
                        xmlns="http://www.w3.org/2000/svg"
                        width="16"
                        height="16"
                      >
                        <path
                          fill-rule="evenodd"
                          d="M12.651 5.47h-.001l.001.001Zm0 0 .708-.708C15.061 6.279 16 8 16 8s-3 5.5-8 5.5a7.03 7.03 0 0 1-2.79-.588l.77-.772c.63.227 1.304.36 2.02.36 2.119 0 3.879-1.168 5.168-2.457a13.187 13.187 0 0 0 1.465-1.755L14.828 8a13.13 13.13 0 0 0-1.66-2.043 12.125 12.125 0 0 0-.517-.486Zm1.703-3.116-12 12-.708-.708 12-12 .708.708ZM2.641 11.238C.94 9.72 0 8 0 8s3-5.5 8-5.5c.96.003 1.91.203 2.79.588l-.77.771A5.944 5.944 0 0 0 8 3.5c-2.12 0-3.879 1.168-5.168 2.457A13.134 13.134 0 0 0 1.172 8c.058.087.122.183.195.288.335.48.83 1.12 1.465 1.755.165.165.337.328.517.486l-.708.709Zm2.062-2.062a3.5 3.5 0 0 1 4.474-4.474l-.823.823a2.5 2.5 0 0 0-2.83 2.829l-.821.822Zm2.943 1.299-.822.822a3.5 3.5 0 0 0 4.474-4.474l-.823.823a2.5 2.5 0 0 1-2.83 2.829Z"
                          clip-rule="evenodd"
                        />
                      </svg>
                    </span>
                  </div>
                </div>

                <router-link
                  to="/author/forgot-password"
                  class="block text-xs text-right font-normal text-gray-500 hover:underline"
                  >Forget Password</router-link
                >
              </div>
              <br />
              <div>
                <BLUIButton
                  background="tw-bg-gray-600"
                  label="Login"
                  variant="primary"
                  :loading="isAuthenticating"
                  full-width
                  @click.prevent="onSubmit"
                />
                <span
                  class="block text-sm font-medium text-center text-gray-500 mb-1"
                  >OR</span
                >
                <BLUIButton
                  background="tw-bg-blue-600"
                  label="Register For New Account"
                  variant="primary-quiet"
                  :disabled="!allowCreateUser"
                  @click.prevent="moveToSelfRegistration"
                  full-width
                />
              </div>
            </form>
          </div>
        </div>
      </div>

      <div class="hidden lg:block lg:flex-grow">
        <img
          class="object-fill rounded h-screen w-full min-h-[700px]"
          alt="CourseMill Login Image"
          src="/src/assets/img/CM_Login_Image.jpg"
        />
      </div>
    </div>
  </section>
</template>
<script setup lang="ts">
import { ref, computed, inject } from 'vue';
import axios from '@/services/REST';
import { useRouter } from 'vue-router';
import { BLUIButton } from '@blue-lightning/ui-components';

const router = useRouter();
const username = ref('');
const password = ref('');
const showPassword = ref(false);
const loginError = ref(false);
const isAuthenticating = ref(false);
const allowCreateUser = ref(true);
const authLogo = ref('');
const authorName = ref('');

const invalidLogin = ref(false);
const token = ref(null);
const $cookies = inject<VueCookies>('$cookies');

function onSubmit() {
  loginError.value = false;

  if (username.value && password.value) {
    invalidLogin.value = false;
    isAuthenticating.value = true;

    const payload = {
      email: username.value,
      password: password.value,
    };

    axios
      .post('/auth/login', payload)
      .then((response) => {
        if (response?.data?.data?.token) {
          invalidLogin.value = false;
          token.value = response.data.data.token;

          if ($cookies) {
            $cookies.set(
              'SESScad1707c10a7cd7c31b10ef6',
              response.data.data.token
            );
          }

          router.push({ name: 'home' });
        } else {
          invalidLogin.value = true;
        }
      })
      .catch((error) => {
        invalidLogin.value = true;
        console.error(error);
      })
      .finally(() => {
        isAuthenticating.value = false;
      });
  } else {
    invalidLogin.value = true;
  }
}

let isLoginFormValid = computed(() => {
  return username.value && password.value;
});

function moveToSelfRegistration() {
  router.push({ name: 'self-registration' });
}
</script>
