<template>
  <div>
    <div id="mySidenav" class="sidenav" :class="openMenu ? 'sidenavOpen' : ''">
      <!-- <a href="javascript:void(0)" class="closebtn" @click="closeNav()">
        <i class="fas fa-times"></i></a> -->
      <a href="#"><i class="fas fa-home"></i> Home </a>
      <a href="#"><i class="fas fa-cog"></i> Settings </a>
      <a href="#"><i class="fas fa-chart-line"></i> Statistics </a>
    </div>
  </div>
  <!--menu end-->
</template>

<script>
import "@/assets/main.css";
export default {
  name: "Menu",
  props: {
    openMenu: Boolean,
  },

  methods: {
    // openNav() {
    // console.log("Clicked", this.openMenu), (this.openMenu = true);
    // this.openMenu = !this.openMenu;
    // },
    // closeNav() {
    // this.openMenu = false;
    // console.log("Clicked", this.openMenu), (this.openMenu = false);
    // },
  },
};
</script>

<style scoped>
</style>