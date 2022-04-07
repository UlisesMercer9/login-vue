<template>
    <div>
        <navbar></navbar>
<div class="min-h-full flex flex-col justify-center py-12 sm:px-6 lg:px-8">
  <div class="mt-8 sm:mx-auto sm:w-full sm:max-w-md shadow-lg">
    <div class="bg-white py-8 px-4 shadow sm:rounded-lg sm:px-10">
      <form class="space-y-6">
        <div>
          <label for="name" class="block text-sm font-medium text-gray-700"> Username </label>
          <div class="mt-1">
            <input id="name" v-model="user.username" name="name" type="text" required class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
            <span v-if="v$.user.username.$error" class="text-red-600 text-xs">
                {{ v$.user.username.$errors[0].$message }}
            </span>
          </div>
        </div>
        <div>
          <label for="email" class="block text-sm font-medium text-gray-700"> Email address </label>
          <div class="mt-1">
            <input id="email" v-model="user.email"  name="email" type="email" autocomplete="email" required class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
            <span v-if="v$.user.email.$error" class="text-red-600 text-xs">
                {{ v$.user.email.$errors[0].$message }}
            </span>
          </div>
        </div>

        <div>
          <label for="password" class="block text-sm font-medium text-gray-700"> Password </label>
          <div class="mt-1">
            <input id="password" v-model="user.password"  name="password" type="password" autocomplete="current-password" required class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
            <span v-if="v$.user.password.$error" class="text-red-600 text-xs">
                {{ v$.user.password.$errors[0].$message }}
            </span>
          </div>
        </div>

        <div>
          <button :disabled="this.v$.$error" @click="submitForm"  class="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">Sign up</button>
        </div>
      </form>
    </div>
  </div>
</div>

    </div>
</template>

<script>

import Navbar from '@/components/Navbar.vue'
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
        user: {
            username: '',
            email: '',
            password: ''
        }
    }
  },
  methods: {
  	submitForm() {
        this.v$.$validate() 
        if (!this.v$.$error) { 
            localStorage.storedData =  JSON.stringify(this.user);
            this.$router.push({ name: 'profile' })
        } else {
            // alert('Form failed validation')
        }
  	}
  },
  validations() {
    return {
        user: {
            username: { required },
            email: { required },
            password: { required }
        }
    }
  }
}
</script>