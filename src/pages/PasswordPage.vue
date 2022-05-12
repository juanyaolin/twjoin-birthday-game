<template>
  <q-page padding>
    <div class="q-gutter-md row">
      <q-btn label="返回" to="/" />
      <q-input outlined class="col" v-model="max" />
      <q-btn label="取得" color="primary" @click="number = getNumber()" />
    </div>

    <div style="font-size: 10rem" class="text-center">
      {{ number }}
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "PasswordPage",

  setup() {
    const max = ref(1000);
    const number = ref(0);

    function getNumber() {
      return Math.floor(Math.random() * (this.max - 2)) + 2;
    }

    return {
      max,
      number,
      getNumber,
    };
  },
});
</script>
