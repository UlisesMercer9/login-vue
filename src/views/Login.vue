<template>
  <div>
    <navbar></navbar>
    <div class="min-h-full flex">
      <div
        class="
          flex-1 flex flex-col
          justify-center
          py-12
          px-4
          sm:px-6
          lg:flex-none lg:px-20
          xl:px-24
        "
      >
        <div class="mx-auto w-full max-w-sm lg:w-96">
          <div>
            <img
              class="h-12 w-auto"
              src="https://tailwindui.com/img/logos/workflow-mark-indigo-600.svg"
              alt="Workflow"
            />
            <h2 class="mt-6 mb-5 text-3xl font-extrabold text-gray-900">
              Sign in to your account
            </h2>
            <!-- This example requires Tailwind CSS v2.0+ -->
            <div class="bg-white shadow sm:rounded-lg" v-if="error_messages">
                <div class="px-4 py-5 sm:p-6">
                    <div class="mt-1 text-sm">
                    <a href="#" class="font-medium text-red-600 hover:text-red-500"> the credentials are incorrect!!</a>
                    </div>
                </div>
            </div>

          </div>

          <div class="mt-8">
            <div class="mt-6">
              <form @submit.prevent="submitForm" class="space-y-6">
                <div>
                  <label
                    for="email"
                    class="block text-sm font-medium text-gray-700"
                  >
                    Email address
                  </label>
                  <div class="mt-1">
                    <input
                      id="email"
                      name="email"
                      type="email"
                      v-model="user.email"
                      autocomplete="email"
                      class="
                        appearance-none
                        block
                        w-full
                        px-3
                        py-2
                        border border-gray-300
                        rounded-md
                        shadow-sm
                        placeholder-gray-400
                        focus:outline-none
                        focus:ring-indigo-500
                        focus:border-indigo-500
                        sm:text-sm
                      "
                    />
                    <span v-if="v$.user.email.$error" class="text-red-600 text-xs">
                        {{ v$.user.email.$errors[0].$message }}
                    </span>
                  </div>
                </div>

                <div class="space-y-1">
                  <label
                    for="password"
                    class="block text-sm font-medium text-gray-700"
                  >
                    Password
                  </label>
                  <div class="mt-1">
                    <input
                      id="password"
                      name="password"
                      type="password"
                      v-model="user.password"
                      autocomplete="current-password"
                      class="
                        appearance-none
                        block
                        w-full
                        px-3
                        py-2
                        border border-gray-300
                        rounded-md
                        shadow-sm
                        placeholder-gray-400
                        focus:outline-none
                        focus:ring-indigo-500
                        focus:border-indigo-500
                        sm:text-sm
                      "
                    />
                    <span v-if="v$.user.password.$error" class="text-red-600 text-xs">
                        {{ v$.user.password.$errors[0].$message }}
                    </span>
                  </div>
                </div>

                <div class="flex items-center justify-between">
                  <div class="flex items-center">
                    <input
                      id="remember-me"
                      name="remember-me"
                      type="checkbox"
                      class="
                        h-4
                        w-4
                        text-indigo-600
                        focus:ring-indigo-500
                        border-gray-300
                        rounded
                      "
                    />
                    <label
                      for="remember-me"
                      class="ml-2 block text-sm text-gray-900"
                    >
                      Remember me
                    </label>
                  </div>

                  <div class="text-sm">
                    <a
                      href="#"
                      class="font-medium text-indigo-600 hover:text-indigo-500"
                    >
                      Forgot your password?
                    </a>
                  </div>
                </div>

                <div>
                  <button
                    :disabled="this.v$.$error"
                    class="
                      w-full
                      flex
                      justify-center
                      py-2
                      px-4
                      border border-transparent
                      rounded-md
                      shadow-sm
                      text-sm
                      font-medium
                      text-white
                      bg-indigo-600
                      hover:bg-indigo-700
                      focus:outline-none
                      focus:ring-2
                      focus:ring-offset-2
                      focus:ring-indigo-500
                    "
                  >
                    Sign in
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
      <div class="hidden lg:block relative w-0 flex-1">
        <img
          class="absolute inset-0 h-full w-full object-cover"
          src="https://images.unsplash.com/photo-1505904267569-f02eaeb45a4c?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1908&q=80"
          alt=""
        />
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import useValidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";

export default {
  components: {
    Navbar
  },
  data(){
    return {
        v$: useValidate(),
        isDisabled: false,
        currentUser: null,
        user: {
            email: '',
            password: ''
        },
        error_messages: false
    }
  },
  methods: {
  	submitForm() {
        this.v$.$validate()
        if (!this.v$.$error) {
            if(this.currentUser.email === this.user.email && this.currentUser.password === this.user.password ) {
                this.$router.push({ name: 'profile' })
            } else {
                this.error_messages = true
            }
        } else {
            // alert('Form failed validation')
        }
  	}
  },
  validations() {
    return {
        user: {
            email: { required },
            password: { required }
        }
    }
  },
  created() {
    this.currentUser = JSON.parse(localStorage.getItem('storedData'))
  },
}
</script>