<template>
  <div>
    <div id="mySidenav" class="sidenav" :class="openMenu ? 'sidenavOpen' : ''">
      <a href="javascript:void(0)" class="closebtn" @click="closeNav()"
        ><i class="fas fa-times"></i
      ></a>
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
  name: "Child",
  props: {
    openMenu: false,
  },

  methods: {
    // openNav() {
    //   console.log("Clicked", this.openMenu), (this.openMenu = true);
    // },
    closeNav() {
      this.openMenu = false;
    },
  },
};
</script>

<style scoped>
</style>