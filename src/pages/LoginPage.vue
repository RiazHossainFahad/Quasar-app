<template>
  <q-page padding>
    <div class="header">
      <h4>LOGIN</h4>
    </div>

    <div class="column flex-center">
      <q-form
        @submit="onSubmit"
        class="q-gutter-md"
      >
        <q-input
          class="input"
          v-model="email"
          label="EMAIL"
          stack-label
          lazy-rules
          :rules="[ val => val && val.length > 0 || 'Please type email-address!']"
        />

        <q-input
          class="input"
          v-model="password"
          label="PASSWORD"
          stack-label
          :type="isPwd ? 'password' : 'text'"
          lazy-rules
          :rules="[
            val => val !== null && val !== '' || 'Empty password!'
          ]"
        >
          <template v-slot:append>
            <q-icon
              :name="isPwd ? 'visibility_off' : 'visibility'"
              class="cursor-pointer"
              @click="isPwd = !isPwd"
            />
          </template>
        </q-input>

        <div align="right">
          <q-btn label="Login" type="submit" color="primary" no-caps/>
        </div>

        <div>
          <span class="subtitle2">Don't have an account?
            <router-link to='/register' class="blue"
              style="text-decoration: none">REGISTER
            </router-link>
          </span>
        </div>
      </q-form>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'LoginPage',
  data() {
    return {
      email: '',
      password: '',
      isPwd: true,
    };
  },
  methods: {
    onSubmit() {
      this.$q.notify({
        color: 'green-4',
        textColor: 'white',
        position: 'top',
        icon: 'fas fa-check-circle',
        message: 'Form Submitted!!',
      });
    },
  },
};
</script>

<style scoped>
.header{
  margin: 10px 0 0 50px
}

.input{
  width: 450px
}
@media screen and (max-width: 536px){
.input{
  width: 300px
}
}
</style>
