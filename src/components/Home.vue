<template>
  <div id="wrapper">
    <Menu :openMenu="openMenu" />

    <div id="main" :class="openMenu ? 'mainOpen' : ''">
      <div class="header">
        <a
          ><span
            style="font-size: 30px; cursor: pointer"
            @click="openNav()"
            aria-label="open menu"
            >&#9776;
          </span></a
        >
        <Header data="Company Logo" />
      </div>
      <!--header end-->

      <AddTitle />
    </div>
    <!--main end-->
  </div>
  <!--wrapper end-->
</template>


<script>
import "@/assets/main.css";
import Menu from "./Menu";
import Header from "./Header";
import AddTitle from "./AddTitle";
export default {
  name: "Home",
  components: { Menu, Header, AddTitle },

  data() {
    return {
      openMenu: false,
          
    };
  },

  methods: {
    openNav() {
      console.log("Clicked", this.openMenu), (this.openMenu = true);
    },
    // closeNav() {
    //   this.openMenu = false;
    // },
  },
};
</script>

<style scoped>
</style>
