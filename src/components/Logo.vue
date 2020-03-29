<template>
  <div class="logo-container">
    <img :src="imgsrc" :alt="imgalt" :class="{'has-error':hasError}" />
  </div>
</template>

<script>
import LogoImg from "../assets/logo.png";
export default {
  name: "logo",
  data: () => {
    return {
      imgsrc: LogoImg,
      imgalt: "No image",
      isActive: true,
      hasError: true
    };
  },
  methods: {
    toast: () => {
      alert();
    }
  }
};
</script>

<style>
.logo-container {
  padding: 12px;
  display: flex;
  justify-content: center;
}
img {
  width: 85px;
}
</style>