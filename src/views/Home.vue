<template>
  <Quizz />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Quizz from "../components/Quizz.vue";
export default defineComponent({
  name: "Home",
  components: {
    Quizz,
  },
});
</script>
