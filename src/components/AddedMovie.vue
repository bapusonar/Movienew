<template>
  <div>
    <!-- ADD MOVIE to HOME PAGE START -->
    <div id="addedMovie">
      <div
        class="fetch-movie-div"
        v-for="(item, index) in favMovie"
        :key="index"
      >
        <div class="fetch-movie-div-info">
          <div class="heightdiv">
            <img :src="item.Poster" />
            <h5><span>Title: </span> {{ item.Title }}</h5>
          </div>
          <a @click="openmoviePopup(index)" href="#" class="btn-link"
            >Movie Details</a
          >
        </div>
      </div>
    </div>
    <!--ADD MOVIE to HOME PAGE END-->

    <!--Movie Details POPUP START -->
    <div id="myModalNew" class="modal" v-if="showmoviePopup">
      <!-- v-if="showmoviePopup"> -->
      <!-- Modal content -->
      <div class="modal-content">
        <div class="modal_head">
          <span class="exitcls backbutton" @click="closemoviePopup">Back</span>
          <div class="movieheading">Movie Details</div>
          <div class="info-page">
            <div class="info-page-img-divleft">
              <img :src="singleMovie.Poster" />
            </div>
            <div class="info-page-img-divright">
              <h5>{{ singleMovie.Title }}</h5>
              <ul class="info-list">
                <li><strong>Genre: </strong>{{ singleMovie.Genre }}</li>
                <li><strong>Runtime: </strong>{{ singleMovie.Runtime }}</li>
                <li>
                  <strong>Released Year: </strong>{{ singleMovie.Released }}
                </li>
                <li><strong>Rated: </strong>{{ singleMovie.Rated }}</li>
                <li>
                  <strong>IMDB Rating: </strong>{{ singleMovie.imdbRating }}
                </li>
                <li>
                  <div class="info-list-div">
                    <h5>Plot</h5>
                    <p>{{ singleMovie.Plot }}</p>
                    <hr />
                    <!-- <a href="" class="buttonlink" @click="closemoviePopup">Back to Home</a> -->
                  </div>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!--Movie Details POPUP END -->
  </div>
</template>

<script>
import axios from "axios";
import "@/assets/main.css";
export default {
  name: "AddedMovie",
  data() {
    return {
      //   show: true,
      //   showPopup: false,
      favMovie: [],
      //   searchText: "",
      items: [],
      newItems: [],
      oldItems: [],
      //   loader: false,
      showmoviePopup: false,
      singleMovie: [],
    };
  },

  computed: {
    setMovie() {
      return sessionStorage.getItem("addeMovie");
    },
  },

  mounted() {
    this.favMovie = JSON.parse(sessionStorage.getItem("addeMovie")) || [];
  },

  methods: {
    // openPopup() {
    //   console.log("Clicked", this.showPopup);
    //   this.showPopup = true;
    // },
    // closePopup() {
    //   this.showPopup = false;
    // },

    openmoviePopup(index) {
      console.log("Clicked", this.showmoviePopup);
      this.showmoviePopup = true;
      let movieId = this.favMovie[index];
      return axios
        .get("http://www.omdbapi.com/?i=" + movieId.imdbID + "&apikey=4c021841")
        .then((response) => {
          this.singleMovie = response.data;
          console.log(this.singleMovie);
        })
        .catch((err) => {
          console.log(err);
        });
    },

    closemoviePopup() {
      this.showmoviePopup = false;
    },

    // getMovies(searchText) {
    //   this.loader = true;
    //   console.log(this.searchText);

    //   return (
    //     axios
    //       .get(
    //         "http://www.omdbapi.com/?s=" +
    //           encodeURI(searchText) +
    //           "&apikey=4c021841"
    //       )
    //       //  var url = "http://www.omdbapi.com/?i=tt3896198&apikey=4c021841"
    //       .then((response) => {
    //         this.items = response.data.Search;
    //         this.loader = false;
    //         console.log(this.items);
    //       })
    //       .catch((err) => {
    //         console.log(err);
    //       })
    //   );
    // },
    //  computed: {
    //     setMovie() {
    //       return this.favMovie = sessionStorage.getItem('addeMovie');
    //     }
    //   },

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

