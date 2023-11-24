<template>
  <div class="login-container">
    <h1 class="login-title">Sign In</h1>
    <div class="flex flex-col gap-2">
      <input
        type="text"
        required
        v-model="username"
        class="border"
        placeholder="Username"
      />
      <input
        type="password"
        required
        v-model="password"
        class="border"
        placeholder="Password"
      />
      <button
        @click="onLogin()"
        :disabled="!isFormValid"
        class="bg-blue-500 text-white py-1 px-3"
      >
        Login
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";
import { useAuthStore } from "@/stores/auth";

const auth = useAuthStore();
const username = ref("");
const password = ref("");
const router = useRouter();

// Check if both username and password are not empty
const isFormValid = () => {
  return username.value.trim() !== "" && password.value.trim() !== "";
};

const onLogin = () => {
  if (isFormValid()) {
    auth.login(username.value); // You may adjust this part according to your authentication logic
    router.push("/");
  } else {
    // Handle invalid login attempt, e.g., show an error message
    alert("Please enter username and password");
  }
};
</script>

<style scoped>
/* Add scoped styles for login.vue */
.login-container {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #fff;
}

.login-title {
  color: #3498db; /* Change title color */
}

.border {
  border: 1px solid #3498db; /* Change border color */
}

.bg-blue-500 {
  background-color: #3498db; /* Change button background color */
}

.bg-blue-500:hover {
  background-color: #1d6fa5; /* Change button background color on hover */
}

.text-white {
  color: #fff; /* Change text color to white */
}
</style>
