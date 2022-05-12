<template>
  <q-page padding>
    <div class="row column flex-center q-gutter-lg q-mt-sm">
      <q-btn size="xl" label="比手畫腳" color="primary" to="/guesstures" />
      <q-btn size="xl" label="終極密碼" color="primary" to="/password" />
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
});
</script>
