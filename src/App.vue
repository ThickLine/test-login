<template>
  <div id="app">
    <div class="grid lg:grid-cols-2 divide-x h-screen">
      <!-- Screen hero -->
      <div class="hidden md:block h-screen hero-cover">
        <img src="https://images.unsplash.com/photo-1493946740644-2d8a1f1a6aff?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1190&q=80"
             alt="cover">
        <div class="absolute grid grid-cols-1 content-center h-full px-20 z-10">
          <!-- Title -->
          <div class="h-1/2 flex flex-col">
            <Logo />
            <div class="my-8"></div>
            <h1 class="text-3xl font-bold text-white">Your Product Our Priority,</h1>
            <h2 class="text-3xl font-bold text-white">Shipment made simple.</h2>
          </div>

          <div class="my-8"></div>

          <!-- Signup Button -->
          <div class="h-1/2 flex flex-col justify-start">
            <p class="text-xl text-white">Not a member yet?</p>
            <div class="my-2"></div>
            <p class="text-sm text-white">
              Please use your and company information to Create Account
            </p>
            <div class="my-4"></div>
            <MainButton text="Create Account" />
          </div>
        </div>
      </div>

      <div class="h-screen grid grid-cols-1 h-full">
        <!-- Small screen hero -->
        <div class="block md:hidden hero-cover flex justify-center">
          <img src="https://images.unsplash.com/photo-1493946740644-2d8a1f1a6aff?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1190&q=80"
               alt="cover">
          <div class="h-full w-full flex flex-col justify-center items-center px-5 container text-center z-10 my-5">
            <Logo width="210" />
            <div class="my-4"></div>
            <h1 class="text-xxs font-bold text-white">
              Built for Logistics Professionals, Perfected for your Business
            </h1>
            <div class="my-2"></div>
            <div class="flex flex-col items-center">
              <p class="text-white">Not a member yet?</p>
              <p class="text-xxs text-white">
                Please use your and company information to Create Account
              </p>
              <div class="my-4"></div>
              <MainButton text="Create Account" />
            </div>
          </div>
        </div>

        <!-- Form -->
        <form @submit.prevent="checkForm"
              method="POST"
              class="flex flex-col justify-center">
          <div class="h-5/6 lg:h-1/3 form-check px-5 md:px-20">
            <h2 class="text-xl md:text-3xl font-bold text-gray-medium">Welcome back!</h2>
            <div class="my-2"></div>
            <div class="text-sm md:text-xl">Please login to your account</div>
            <div class="my-8"></div>
            <!-- Error list -->
            <p v-if="errors.length"
               class="my-2">
              <strong>Please correct the following error(s):</strong>
            <ul class="text-red ml-2 text-sm">
              <li v-for="error in errors"
                  :key="error">{{ error }}</li>
            </ul>
            </p>
            <!-- Email input -->
            <Input label="E-mail"
                   type="email"
                   v-model="form.email"
                   placeholder="e-mail" />
            <!-- Password input -->
            <Input label="Password"
                   type="password"
                   v-model="form.password"
                   placeholder="password"
                   isPassword="true" />
            <div class="my-4"></div>
            <div class="flex justify-between">
              <Checkbox label="Keep me logged in"
                        @input="form.keepLoggedIn = !form.keepLoggedIn" />
              <div class="text-gray-dark text-sm">Forgot password?</div>
            </div>
            <div class="my-4"></div>
            <div class="flex justify-end">
              <MainButton text="Log in"
                          @click="checkForm()"
                          :type="buttonType" />
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Logo from "./components/Logo.vue";
import MainButton from "./components/MainButton.vue";
import Input from "./components/Input.vue";
import Checkbox from "./components/Checkbox.vue";
import ILoginForm from "./type/form/login/ILoginForm";
import ButtonEnum from "./enums/buttons";
import { LOGIN_FORM } from "./mock/form";
import { REGEX_EMAIL, REGEX_PASSWORD } from "./constants/validation";

@Component({
  components: {
    MainButton,
    Logo,
    Input,
    Checkbox,
  },
})
export default class App extends Vue {
  public errors: string[] = [];

  public get buttonType() {
    return ButtonEnum.yellow;
  }

  public form: ILoginForm = JSON.parse(JSON.stringify(LOGIN_FORM))

  // Validate form input
  public async checkForm(): Promise<void> {
    this.errors = []
    if (!this.form.email.match(REGEX_EMAIL)) {
      this.errors.push('Must be a email')

    }

    if (!this.form.password.match(REGEX_PASSWORD)) {
      this.errors.push('Must be a valid password')

    }

    if (!this.errors.length) {
      return this.onSubmit(this.form)
    }
  }

  private onSubmit(data: ILoginForm): void {
    return alert("Logged in successfully");
  }

}
</script>

