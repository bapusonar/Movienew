<template>
  <div id="wrapper">
    <Menu :openMenu="openMenu" />

    <div id="main" :class="openMenu ? 'mainOpen' : ''">
      <div class="header">
        <a
          ><span
            @click="openNav()"
            aria-label="open menu"
            :class="openMenu ? 'barclose' : 'baropen'"
          ></span
        ></a>
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
    }
  },

  methods: {
    openNav() {
      // console.log("Clicked", this.openMenu), (this.openMenu = true);
      this.openMenu = !this.openMenu;
    },
    // closeNav() {
    //   this.openMenu = true;
    // },
  },
};
</script>

<style scoped>
.baropen::before {
  color: black;
  width: 20px;
  font-size: 30px;
  cursor: pointer;
  display: block;
  /* content:'/&#9776;' */
  content: "\2630";
  /* content: '\292B'; */
}

/* .baropen::before { 
  content: '\2630';
} */

.barclose::before {
  color: black;
  width: 20px;
  display: block;
  font-size: 40px;
  cursor: pointer;
  /* content:'/&#9776;' */
  /* content: '\2630'; */
  content: "\292B";
}

.x {
  position: relative;
  width: 23px;
  height: 23px;
  border: 2px solid #eef5df;
  background-color: #ff5248;
  border-radius: 50%;
}
.x::before,
.x::after {
  position: absolute;
  top: 10px;
  left: 5px;
  width: 13px;
  height: 3px;
  content: "";
  background-color: #eef5df;
  display: none;
}
.x::before {
  -ms-transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
}
.x::after {
  -ms-transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
}
.x:hover {
  cursor: pointer;
}
.x:hover::before,
.x:hover::after {
  display: block;
}
</style>
