<template>
  <div class="d-flex vh-100 overflow-hidden">
    <!-- Authentication Form (if not authenticated) -->
    <div
      v-if="!isAuthenticated"
      class="d-flex justify-content-center align-items-center text-black w-100 min-vh-100"
    >
      <div
        class="text-center p-4 rounded shadow-lg"
        style="width: 100%; max-width: 400px"
      >
        <h3 class="mb-4">Are you a real admin?</h3>

        <!-- Name Input -->
        <div class="input-group w-100">
          <span class="input-group-text"><i class="fas fa-user"></i></span>
          <input
            v-model="name"
            type="text"
            class="form-control mb-1"
            placeholder="Enter your name"
            :disabled="isLoading"
            :class="{ 'is-invalid': loginFailed }"
          />
        </div>

        <!-- Password Input -->
        <div class="input-group w-100">
          <span class="input-group-text"><i class="fas fa-lock"></i></span>
          <input
            v-model="password"
            type="password"
            class="form-control mb-3"
            placeholder="Enter password"
            :disabled="isLoading"
            :class="{ 'is-invalid': loginFailed }"
          />
        </div>

        <!-- Login Button -->
        <button
          class="btn btn-primary w-100"
          @click="authenticate"
          :disabled="isLoading"
        >
          Login
        </button>

        <!-- Error Message -->
        <p v-if="loginFailed" class="text-danger mt-2">Invalid credentials.</p>

        <!-- Loading Spinner -->
        <div v-if="isLoading" class="mt-3">
          <i class="fas fa-spinner fa-spin text-black"></i> Checking...
        </div>
      </div>
    </div>

    <!-- Dashboard (if authenticated) -->
    <div v-else class="d-flex w-100">
      <!-- Sidebar -->
      <div class="bg-dark text-white d-flex flex-column" style="width: 230px">
        <div class="bg-dark p-3 text-center">
          <a href="#" class="h4 m-0 text-decoration-none">Paws Kingdoms</a>
        </div>
        <nav class="nav flex-column flex-grow-1 py-3">
          <router-link
            :to="{ name: 'home' }"
            class="nav-link text-white px-3 py-2 d-flex align-items-center"
            exact-active-class="active"
          >
            <i class="fas fa-cat me-2"></i>
            <span>Home</span>
          </router-link>

          <router-link
            :to="{ name: 'catfoods.index' }"
            class="nav-link text-white px-3 py-2 d-flex align-items-center"
            exact-active-class="active"
          >
            <i class="fas fa-cat me-2"></i>
            <span>Edit Menu Cat Foods</span>
          </router-link>

          <router-link
            :to="{ name: 'cattoys.index' }"
            class="nav-link text-white px-3 py-2 d-flex align-items-center"
            exact-active-class="active"
          >
            <i class="fas fa-cat me-2"></i>
            <span>Edit Menu Cat Toys</span>
          </router-link>
        </nav>
      </div>

      <!-- Main Content Area -->
      <div class="flex-grow-1 d-flex flex-column overflow-hidden">
        <!-- Navbar -->
        <header class="text-black py-3">
          <div
            class="container-fluid d-flex justify-content-between align-items-center"
          >
            <h1 class="h5 mb-0 font-weight-bold">Welcome to Admin Dashboard</h1>
            <div class="d-none d-md-block">
              <a href="/" class="btn btn-danger btn-sm rounded-pill px-3 py-2">
                <i class="bi bi-box-arrow-right me-2"></i>
                Logout
              </a>
            </div>
          </div>
        </header>

        <!-- Content Wrapper -->
        <main class="flex-grow-1 overflow-auto p-4">
          <router-view v-slot="{ Component }">
            <transition name="fade" mode="out-in">
              <component :is="Component" />
            </transition>
          </router-view>
        </main>
      </div>
    </div>

    <!-- Welcome Notification -->
    <div
      v-if="showWelcome"
      class="position-fixed top-0 end-0 m-3 bg-success text-white p-3 rounded"
      style="z-index: 1050"
    >
      Welcome, {{ name }}!
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "", // Store the user's name
      password: "", // Store the password input
      isAuthenticated: false, // Track authentication status
      loginFailed: false, // Track failed login attempts
      isLoading: false, // Track the loading status
      showWelcome: false, // Track the visibility of the welcome notification
    };
  },
  methods: {
    // Handle login
    async authenticate() {
      this.isLoading = true; // Show loading animation

      setTimeout(() => {
        if (this.password === "1") {
          this.isAuthenticated = true; // Successful authentication
          this.loginFailed = false; // Reset login failure flag
          this.showWelcomeNotification(); // Show the welcome notification
        } else {
          this.loginFailed = true; // Failed login
        }
        this.isLoading = false; // Hide loading animation
      }, 1500); // Simulate a loading delay (1.5 seconds)
    },

    // Show welcome notification for 3 seconds
    showWelcomeNotification() {
      this.showWelcome = true; // Show the welcome notification
      setTimeout(() => {
        this.showWelcome = false; // Hide the notification after 3 seconds
      }, 3000);
    },
  },
};
</script>
