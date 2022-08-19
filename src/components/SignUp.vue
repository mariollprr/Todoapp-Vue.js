<template>
  <section class="vh-50 gradient-custom">
    <div class="container py-5 h-50">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-12 col-md-8 col-lg-6 col-xl-5">
          <div class="card bg-dark text-white" style="border-radius: 1rem">
            <div class="card-body p-5 text-center">
              <div class="mb-md-5 mt-md-4 pb-5">
                <h1 class="mb-2">
                  OhMy<span class="fw-bold" id="texto"
                    ><strong><i>Tasks!</i></strong></span
                  >
                </h1>
                <h4 class="text-white-50 mb-5">
                  Always now what's next
                  <img src="../assets/check.svg" alt="check" />
                </h4><aside>
                  </aside>
                <div class="form-outline form-white mb-4">
                  <input
                    type="email"
                    id="typeEmailX"
                    class="form-control form-control-lg"
                    placeholder="Email"
                  />
                  <label class="form-label" for="typeEmailX">Email</label>
                </div>

                <div class="form-outline form-white mb-4">
                  <input
                    type="password"
                    id="typePasswordX"
                    class="form-control form-control-lg"
                    placeholder="Password"
                  />
                  <label class="form-label" for="typePasswordX">Password</label>
                </div>

                <div class="form-outline form-white mb-4">
                  <input
                    type="confirmPassword"
                    id="typePasswordX"
                    class="form-control form-control-lg"
                    placeholder="Confirm your password"
                  />
                  <label class="form-label" for="typePasswordX">Confirm your password</label>
                </div>

                <button class="btn btn-outline-light btn-lg px-5" type="submit">
                  Sign In
                </button>
              </div>

              <div>
                <p class="mb-0">
                  Don't have an account?
                  <a href="/auth/sign-in" class="text-white-50 fw-bold">Sign In</a>
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import PersonalRouter from "./PersonalRouter.vue";

// Route Variables
const route = "/auth/sign-in";
const buttonText = "Test the Sign in Route";

// Input Fields
const email = ref("");
const password = ref("");
// Error Message
const errorMsg = ref("");
// Show hide password variable
const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
);
const hidePassword = ref(true);
// Show hide confrimPassword variable

// Router to push user once SignedUp to Log In

// Arrow function to SignUp user to supaBase with a timeOut() method for showing the error
</script>

<style></style>
