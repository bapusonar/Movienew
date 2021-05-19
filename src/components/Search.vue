<template>
  <div>
    <!--SEARCH MOVIE CONTENT START-->
    <div class="form-group">
      <div class="example" style="margin: auto; max-width: 600px">
        <input
          type="text"
          id="searchText"
          placeholder="Search Movie.."
          aria-label="Search"
          v-model="searchText"
        />
        <button type="submit" @click="getMovies(searchText)">
          <i class="fa fa-search" aria-hidden="true"></i>
        </button>
      </div>

      <div class="datafetch">
        <div v-if="loader">
          <img
            :src="'https://media3.giphy.com/media/3oEjI6SIIHBdRxXI40/200.gif'"
          />
        </div>
        <div id="movies" v-else class="datafetch-movie">
          <div>
            <div
              class="fetch-movie-div"
              v-for="(item, index) in items"
              :key="index"
              @click="add(index)"
            >
              <div class="fetch-movie-div-info">
                <img :src="item.Poster" />
                <h5><span>Title: </span> {{ item.Title }}</h5>
                <!-- <a href="#" item.imdbID>Movie Details</a> -->
              </div>
            </div>
          </div>
        </div>
      </div>
      <!--datafetch end-->
    </div>
    <!--form group end-->
    <!--SEARCH MOVIE CONTENT END-->

 

  </div>
</template>

<script>
import axios from "axios";
import "@/assets/main.css";
export default {
  name: "Search",
  data() {
    return {
      show: true,
    //   showPopup: false,
      favMovie: [],
      searchText: "",
      items: [],
      newItems: [],
      oldItems: [],
      loader: false,
    //   showmoviePopup: false,
    //   singleMovie: [],
    };
  },

//   mounted() {
//     this.favMovie = JSON.parse(sessionStorage.getItem("addeMovie")) || [];
//   },

  methods: {
    // openPopup() {
    //   console.log("Clicked", this.showPopup);
    //   this.showPopup = true;
    // },
    // closePopup() {
    //   this.showPopup = false;
    // },

    // openmoviePopup(index) {
    //   console.log("Clicked", this.showmoviePopup);
    //   this.showmoviePopup = true;
    //   let movieId = this.favMovie[index];
    //   return axios
    //     .get("http://www.omdbapi.com/?i=" + movieId.imdbID + "&apikey=4c021841")
    //     .then((response) => {
    //       this.singleMovie = response.data;
    //       console.log(this.singleMovie);
    //     })
    //     .catch((err) => {
    //       console.log(err);
    //     });
    // },

    // closemoviePopup() {
    //   this.showmoviePopup = false;
    // },

    getMovies(searchText) {
      this.loader = true;
      console.log(this.searchText);

      return (
        axios
          .get(
            "http://www.omdbapi.com/?s=" +
              encodeURI(searchText) +
              "&apikey=4c021841"
          )
          //  var url = "http://www.omdbapi.com/?i=tt3896198&apikey=4c021841"
          .then((response) => {
            this.items = response.data.Search;
            this.loader = false;
            console.log(this.items);
          })
          .catch((err) => {
            console.log(err);
          })
      );
    },

    add(index) {
      this.newItems = this.items[index];
       this.oldItems.push(this.newItems);
      this.favMovie = this.oldItems;
      console.log(this.oldItems, "");

      sessionStorage.setItem("addeMovie", JSON.stringify(this.oldItems));
    },
  },
};
</script>


