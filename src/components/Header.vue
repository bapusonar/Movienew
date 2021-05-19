<template>
  <div>
    <a class="logoClass">{{ data }}</a>
  </div>
</template>

<script>
import "@/assets/main.css";
export default {
  name: "Header",
  props: {
    data: String,
  },
};
</script>

