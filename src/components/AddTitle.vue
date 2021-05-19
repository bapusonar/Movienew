<template>
  <div>
    <div class="container">
      <div id="myBtn" @click="openPopup">
        <div class="titleDiv">
          <p>
            Add Title <br />
            +
          </p>
        </div>
      </div>

      <div id="myModal" class="modal" v-if="showPopup">
        <!-- v-if="showPopup"> -->
        <!-- Modal content -->
        <div class="modal-content">
          <div class="modal_head">
            <span class="exitcls" @click="closePopup">&times;</span>
            <h5>Add Title</h5>
          </div>

          <Search />
        </div>
        <!--modal content end -->
      </div>
      <!--the modal end-->

        <AddedMovie />

    </div>
    <!--container end-->
  </div>
</template>

<script>
// import axios from "axios";
import "@/assets/main.css";
import Search from "./Search";
import AddedMovie from "./AddedMovie";
export default {
  name: "AddTitle",
  components: { Search, AddedMovie },
  data() {
    return {
      show: true,
      showPopup: false,
      //   favMovie: [],
      //   searchText: "",
        // items: [],
      //   newItems: [],
      //   oldItems: [],
      //   loader: false,
      //   showmoviePopup: false,
      //   singleMovie: [],
    };
  },

  //   mounted() {
  //     this.favMovie = JSON.parse(sessionStorage.getItem("addeMovie")) || [];
  //   },

  methods: {
    openPopup() {
      console.log("Clicked", this.showPopup);
      this.showPopup = true;
    },
    closePopup() {
      this.showPopup = false;
    },

    //     openmoviePopup(index) {
    //       console.log("Clicked", this.showmoviePopup);
    //       this.showmoviePopup = true;
    //       let movieId = this.favMovie[index];
    //       return axios
    //         .get("http://www.omdbapi.com/?i=" + movieId.imdbID + "&apikey=4c021841")
    //         .then((response) => {
    //           this.singleMovie = response.data;
    //           console.log(this.singleMovie);
    //         })
    //         .catch((err) => {
    //           console.log(err);
    //         });
    //     },

    //     closemoviePopup() {
    //       this.showmoviePopup = false;
    //     },

    //     getMovies(searchText) {
    //       this.loader = true;
    //       console.log(this.searchText);

    //       return (
    //         axios
    //           .get(
    //             "http://www.omdbapi.com/?s=" +
    //               encodeURI(searchText) +
    //               "&apikey=4c021841"
    //           )
    //           //  var url = "http://www.omdbapi.com/?i=tt3896198&apikey=4c021841"
    //           .then((response) => {
    //             this.items = response.data.Search;
    //             this.loader = false;
    //             console.log(this.items);
    //           })
    //           .catch((err) => {
    //             console.log(err);
    //           })
    //       );
    //     },

    //     add(index) {
    //       this.newItems = this.items[index];
    //       //  console.log(index, this.newItems)
    //       //  this.oldItems = JSON.parse(sessionStorage.getItem("addeMovie")) || [];
    //       this.oldItems.push(this.newItems);
    //       this.favMovie = this.oldItems;
    //       console.log(this.oldItems, "");

    //       sessionStorage.setItem("addeMovie", JSON.stringify(this.oldItems));
    //     },
  },
};
</script>


