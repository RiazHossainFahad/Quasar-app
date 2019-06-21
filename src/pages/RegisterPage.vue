/* eslint-disable no-useless-escape */
/* eslint-disable prefer-const */
<template>
  <q-page padding>
    <div class="header">
      <h4>REGISTER</h4>
    </div>

    <div class="column flex-center">
      <q-form
        @submit="onSubmit"
        class="q-gutter-xs"
      >
        <q-input
          class="input"
          v-model="fname"
          label="FIRST NAME"
          stack-label
          :rules="[ val => val && val.length > 0 || 'Please type first name',
                    val => validateName || 'Invalid Name!',
                    val => val && val.length > 1 || 'type a correct name'
                  ]"
        />
        <q-input
          class="input"
          v-model="lname"
          label="LAST NAME"
          stack-label
          :rules="[ val => val && val.length > 0 || 'Please type last name',
                    val => validateLastName || 'Invalid Name!',
                    val => val && val.length > 1 || 'type a correct name'
                  ]"
        />
        <q-input
          class="input"
          v-model="email"
          label="EMAIL"
          stack-label
          :rules="[ val => val && val.length > 0 || 'Please type email-address',
                    val => validateEmail || 'Invalid Email address',
                  ]"
        />

        <q-input
          class="input"
          v-model="password"
          label="PASSWORD"
          stack-label
          :type="isPwd ? 'password' : 'text'"
          :rules="[
            val => val !== null && val !== '' || 'Empty password',
            val => val.length > 3 || 'Length is less than 4!',
            val => validatePassword
            || 'Invalid! atleast one capital & small letter, One digit required'
          ]"
        >
          <template v-slot:append>
            <q-icon
              :name="isPwd ? 'visibility_off' : 'visibility'"
              class="cursor-pointer"
              @click="isPwd = !isPwd"
            />
          </template>

          <q-tooltip
            transition-show="rotate"
            transition-hide="rotate"
            anchor="top middle" self="bottom middle" :offset="[3, 3]"
            >
             Format: Atleast one capital & small letter, One digit required
          </q-tooltip>

        </q-input>

        <q-input
          class="input"
          v-model="reTypePassword"
          label="RE TYPE PASSWORD"
          stack-label
          :type="isPwdC ? 'password' : 'text'"
          :rules="[
            val => val !== null && val !== '' || 'Empty password',
            val => val.length > 3 || 'Length is less than 4!',
            val => val == password || 'Password mis-matched!'
          ]"
        >
          <template v-slot:append>
            <q-icon
              :name="isPwdC ? 'visibility_off' : 'visibility'"
              class="cursor-pointer"
              @click="isPwdC = !isPwdC"
            />
          </template>
        </q-input>

        <div align="right">
          <q-btn label="Register" type="submit" color="primary" no-caps/>
        </div>

        <div>
          <span class="subtitle2">Already have an account?
            <router-link to='/' class="blue" style="text-decoration: none">LOGIN</router-link>
          </span>
        </div>
      </q-form>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'RegisterPage',
  data() {
    return {
      fname: '',
      lname: '',
      email: '',
      password: '',
      reTypePassword: '',
      isPwd: true,
      isPwdC: true,
      accept: false,
    };
  },
  computed: {
    validateEmail() {
      // eslint-disable-next-line no-useless-escape
      const regex = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return regex.test(this.email);
    },
    validateName() {
      // eslint-disable-next-line no-useless-escape
      const regexname = /[a-zA-Z]/;
      return regexname.test(this.fname);
    },
    validateLastName() {
      // eslint-disable-next-line no-useless-escape
      const regexname = /[a-zA-Z]/;
      return regexname.test(this.lname);
    },
    validatePassword() {
      // eslint-disable-next-line no-useless-escape
      const passEx = /(?=.*\d)(?=.*[a-z])(?=.*[A-Z])/;
      return passEx.test(this.password);
    },
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
