<template>
  <div id="wrapper">
    <div id="mySidenav" class="sidenav" :class="openMenu ? 'sidenavOpen' : '' ">
      <a href="javascript:void(0)" class="closebtn" @click="closeNav()"
        ><i class="fas fa-times"></i
      ></a>
      <a href="#"><i class="fas fa-home"></i> Home Page </a>
      <a href="#"><i class="fas fa-cog"></i> Settings </a>
      <a href="#"><i class="fas fa-chart-line"></i> Statistics </a>
    </div>
    <!--menu end-->

    <div id="main" mainOpen :class="openMenu ? 'mainOpen' : ''">
      <div class="header">
        <a
          ><span
            style="font-size: 30px; cursor: pointer"
            @click="openNav()"
            aria-label="open menu"
            >&#9776;
          </span></a
        >
        <a href="#default" class="logo">CompanyLogo</a>
      </div>
      <!--header end-->

      <Movie />

    </div>
    <!--main end-->
  </div>
  <!--wrapper end-->
</template>


<script>
import Movie from "./Movie";
export default {
  name: "Home",
  components: { Movie },

  data() {
    return {
      openMenu: false,
    };
  },

  methods: {
    openNav() {
      console.log("Clicked", this.openMenu), (this.openMenu = true);
    },
    closeNav() {
      this.openMenu = false;
    },
  },
};
</script>


<style scoped>
#wrapper {
  margin: 0;
  padding: 0;
}

.header {
  overflow: hidden;
  background-color: #f1f1f1;
  padding: 20px 10px;
}

.header a {
  float: left;
  color: black;
  text-align: center;
  padding: 12px;
  text-decoration: none;
  font-size: 18px;
  line-height: 25px;
}

.header a.logo {
  font-size: 25px;
  font-weight: bold;
}

@media screen and (max-width: 500px) {
  .header a {
    float: none;
    display: block;
    text-align: left;
  }

  .header-right {
    float: none;
  }
}

/* header end */

/* Nav bar css*/
.sidenav {
  height: 100%;
  width: 0;
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  background-color: #555;
  overflow-x: hidden;
  transition: 0.5s;
  padding-top: 30px;
}

.sidenavOpen {
  width: 250px;
}
.mainOpen {
  margin-left: 250px;
}

.sidenav a {
  padding: 15px 8px 15px 30px;
  text-decoration: none;
  font-size: 16px;
  color: #fff;
  display: block;
  border-bottom: solid 1px #ccc;
  transition: 0.3s;
  text-align: left;
}

i.fa {
  padding-right: 5px;
}

.sidenav .noborder {
  border: none;
}

.sidenav a:hover {
  color: #f1f1f1;
}

.sidenav .closebtn {
  top: 15px;
  position: absolute;
  right: 10px;
  border: none;
}

.sidenav .exitbtn {
  position: absolute;
  top: 10;
  right: 25px;
  font-size: 36px;
  margin-left: 50px;
}

#main {
  transition: margin-left 0.5s;

  width: 100%;
  /* padding: 16px; */
}

@media screen and (max-height: 450px) {
  .sidenav {
    padding-top: 15px;
  }
  .sidenav a {
    font-size: 18px;
  }
}

/* Nav bar css end */
</style>