<template>
  <q-page padding>
    <div class="column flex-center body-margin">
      <q-form
        @submit="onSubmit"
        class="q-gutter-xl"
      >
        <div style="max-width: 310px">
          <p class="text-weight-bold">
            We have sent you an email with a verification
            code in order to verify your account. Please enter
            it here.
          </p>
        </div>

        <div>
          <q-input
            class="input"
            v-model="vfCode"
            label="Verification Code"
            stack-label
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Please enter the code!']"
          />

          <div>
            <q-btn label="Verify" type="submit" class="q-mt-sm" color="primary" no-caps/>
          </div>

        </div>

        <div>
          <div style="max-width: 310px">
              <p class="text-weight-bold">
                If you did not receive an email within 5 minutes,
                then you could re-generate one.
              </p>
          </div>

          <div>
            <q-btn label="Re-send Code" color="primary" no-caps/>
          </div>

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
      vfCode: '',
    };
  },
  methods: {
    onSubmit() {
      this.$q.notify({
        color: 'green-4',
        textColor: 'white',
        position: 'top',
        icon: 'fas fa-check-circle',
        message: 'Code Submitted!!',
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
  width: 400px
}

.body-margin{
  margin-top: 60px
}

@media screen and (max-width: 536px){
.input{
  width: 300px
}
}
</style>
