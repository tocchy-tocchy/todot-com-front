<template>
  <div class="login userAdmin">
    <form class="form-signin" @submit.prevent="submitForm">
      <!-- <img class="mb-4" src="" alt="" width="72" height="72" /> -->
      <h1 class="h3 mb-3 font-weight-normal">ログインする</h1>
      <h1>現在メンテナンス中です。</h1>
      <label for="name" class="sr-only">ユーザー名</label>
      <input
        v-model="name"
        id="name"
        class="form-control"
        placeholder="ユーザー名"
        required
        autofocus
      />
      <label for="password" class="sr-only">パスワード</label>
      <input
        v-model="password"
        type="password"
        id="password"
        class="form-control"
        placeholder="パスワード"
        required
      />
      <button class="btn btn-lg btn-primary btn-block" type="submit">
        ログイン</button
      ><br />

      <p>あるいは<router-link to="register">登録する</router-link></p>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import goapi from "goAPI";
import VueSession from "vue-session";
export default {
  data() {
    return {
      name: "",
      password: "",
    };
  },
  methods: {
    submitForm() {
      const params = new URLSearchParams();

      params.append("name", this.name);
      params.append("password", this.password);
      axios
        .post(goapi.apiUrl + "/login", params, { withCredentials: true })
        .then((res) => {
          this.$session.set("jwt", response.body.token);
          Vue.http.headers.common["Authorization"] =
            "Bearer " + response.body.token;
          this.$router.push({ name: "Mypage" });
        })
        .catch((error) => {
          alert("現在メンテナンス中です");
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
  color: #42b983;
}
</style>
