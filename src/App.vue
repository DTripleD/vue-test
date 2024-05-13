<template>
  <input type="text" v-model="userName" placeholder="Имя" />
  <input type="password" v-model="userPass" placeholder="Пароль" />
  <input type="email" v-model="userEmail" placeholder="Email" />
  <button @click="sendData">отправить</button>
  <p className="error">{{ error }}</p>

  <div v-if="users.length === 0" className="user">У нас нет пользователей</div>

  <div v-else className="user">У нас {{ users.length }} пользователей</div>

  <User
    v-for="(el, index) in users"
    :key="index"
    :user="el"
    :index="index"
    :deleteUser="deleteUser"
  />
</template>

<script>
import User from "./components/User.vue";

export default {
  components: { User },
  data() {
    return {
      users: [],
      error: "",
      userName: "",
      userPass: "",
      userEmail: "",
    };
  },
  methods: {
    sendData() {
      if (this.userName === "") {
        this.error = "Имя не введено";
        return;
      }

      if (this.userPass === "") {
        this.error = "Пароль не введено";
        return;
      }

      if (this.userEmail === "") {
        this.error = "Email не введено";
        return;
      }

      this.error = "";

      this.users.push({
        name: this.userName,
        password: this.userPass,
        email: this.userEmail,
      });
    },

    deleteUser(index) {
      this.users.splice(index, 1);
    },
  },
};
</script>

<style scoped>
input {
  display: block;
  margin-bottom: 10px;
  border-radius: 3px;
  border: 1px solid silver;
  outline: none;
  padding: 10px 15px;
  background-color: #fafafa;
  color: #333;
}

button {
  border: 0;
  border-radius: 5px;
  outline: none;
  padding: 10px 15px;
  background-color: #6cd670;
  color: #167f3d;
  font-weight: bold;
  cursor: pointer;
  transition: transform 500ms ease;
}

button:hover {
  transform: translateY(-5px);
}

.user {
  width: 500px;
  margin-top: 20px;
  border: 1px solid silver;
  background-color: #e3e3e3;
  color: #222;
  padding: 20px;
  border-radius: 5px;
}
</style>
