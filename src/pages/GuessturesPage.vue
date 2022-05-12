<template>
  <q-page padding>
    <div class="q-gutter-md row flex-center">
      <q-btn label="返回" to="/" />
      <q-btn label="開始" color="primary" @click="startGame()" />
      <q-btn label="跳過" color="negative" @click="nextOne()" />
      <q-btn label="答對" color="positive" @click="nextOne(true)" />
    </div>

    <div class="text-center q-mt-lg" style="font-size: 2.5rem; color: red">
      {{ timeString }}
    </div>

    <div class="text-center q-mt-lg" style="font-size: 1rem">
      跳過：{{ failed }}　答對：{{ correct }}
    </div>

    <div class="text-center q-mt-lg" style="font-size: 7.5rem">
      {{ current }}
    </div>
  </q-page>
</template>

<script>
import { computed, defineComponent, ref } from "vue";
import jsonData from "../../guesstures.json";

let timer;
let data = [];
for (const key in jsonData) {
  if (Object.hasOwnProperty.call(jsonData, key)) {
    const element = jsonData[key];
    data.push(element);
  }
}
console.log(data);
export default defineComponent({
  name: "GuessturesPage",

  setup() {
    const items = ref(data);
    const isStarted = ref(false);
    const current = ref("");
    const used = ref({});
    const time = ref(300);
    const timeString = computed(() => {
      if (time.value == 0) {
        clearInterval(timer);
      }

      let second = time.value % 60;
      let minute = Math.floor(time.value / 60);

      return (
        minute +
        ":" +
        second.toLocaleString("en", {
          minimumIntegerDigits: 2,
          useGrouping: false,
        })
      );
    });
    const correct = ref(0);
    const failed = ref(0);

    function nextOne(isRight = false) {
      let index = Math.floor(Math.random() * items.value.length);
      used.value[current.value] = isRight;
      current.value = items[index];

      items.value.splice(index, 1);
      console.log(items.value);
    }

    function startGame() {
      correct.value = 0;
      failed.value = 0;

      timer = setInterval(() => {
        time.value--;
      }, 1000);

      current.value = items[Math.floor(Math.random() * items.value.length)];
    }

    return {
      items,
      isStarted,
      current,
      used,
      time,
      timeString,
      correct,
      failed,
      nextOne,
      startGame,
    };
  },
});
</script>
