<template>
  <div class="about">
    <h1>This is an login page</h1>

    <div class="row">
      <div class="col"></div>
      <div class="col">
        <form>
          <div class="form-group">
            <label for="exampleInputEmail2">Email adresa</label>
            <input
              v-model="username"
              type="email"
              class="form-control"
              id="exampleInputEmail2"
              aria-describedby="emailHelp"
              placeholder="Enter email*"
            />
            <small id="emailHelp" class="form-text text-muted"
              >*We'll never share your email with anyone else.</small
            >
          </div>

          <div class="form-group">
            <label for="exampleInputPassword2">Lozinka</label>
            <input
              v-model="password"
              type="password"
              class="form-control"
              id="exampleInputPassword2"
              placeholder="Password"
            />
          </div>

          <button
            type="submit"
            @click.prevent="login()"
            class="btn btn-primary"
          >
            Submit
          </button>
        </form>
      </div>

      <div class="col"></div>
    </div>
  </div>
</template>

<script>
import firebase from "@/firebase";
import store from "@/store";

export default {
  name: "login",
  data() {
    return {
      username: "",
      password: "",
    };
  },

  methods: {
    login() {
      console.log("login..." + this.username);

      firebase
        .auth()
        .signInWithEmailAndPassword(this.username, this.password)
        .then((result) => {
          console.log("Uspješna prijava.", result);
          // Postavite vrijednost store.currentUser na email korisnika
          store.currentUser = this.username;
          // Preusmjerite korisnika na "home" stranicu nakon prijave
          this.$router.push({ name: "home" });
        })
        .catch((error) => {
          console.error("Dogodila se pogreška prilikom prijave.", error);
        });
    },
  },
};
</script>
