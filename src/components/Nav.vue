<template>
  <nav class="navbar navbar-expand-lg ">
    <div class="container-fluid">
      <router-link to="/">
        <img 
        src="../assets/nav-logo.png" 
        height="65" 
        alt="OHMT logo" 
        loading="lazy" 
        style="margin-top: -1px;;" />
      </router-link>
      <div class="d-grid gap-2 d-md-flex justify-content-md-end">
        <p id="welcomemsg" class="me-auto">
          <img 
          src="../assets/hand-waving.png" 
          width="22" 
          height="22"
           alt="Hamd Waving Icon" />
          Welcome back, <span>{{ name[0] }}</span>!
        </p>
        <button @click="signOut" type="button" class="btn btn-primary" id="signOut">
          Sign Out
        </button>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";

const route = "/";

const userStore = useUserStore();

const email = userStore.user.email;
// constant that saves the user email and cleans out the @client from the user
const name = email.split("@");

const redirect = useRouter();
const signOut = async () => {
  try {
    // calls the user store and signs out
    await useUserStore().signOut();
    redirect.push({ path: "/auth/login" });
  } catch (error) {
    errorMsg.value = error.message;
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  };
};
</script>

<style scoped>
#welcomemsg {
  margin-top: 20px;
  color: white;
  padding-right: 30px
}

span {
  font-weight: bold;
}

.btn {
  margin-left: 40px;
  margin-top: 0;
  height: min-content;
}
.btn:hover {
  background-color: rgb(202, 3, 3);
  transition: 0.5s;
}
.btn:focus {
  border: rgb(202, 3, 3)
}

.navbar-expand-lg {
  background-color: #2f2e41;
  padding: 0px;
}

@media (max-width: 800px) {
p {
display:none;
}
}
</style>