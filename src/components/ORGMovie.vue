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
        <!--modal content end -->
      </div>
      <!--the modal end-->

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
            <span class="exitcls backbutton" @click="closemoviePopup"
              >Back</span
            >
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
    <!--container end-->
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "ModalPopup",
  data() {
    return {
      show: true,
      showPopup: false,
      favMovie: [],
      searchText: "",
      items: [],
      newItems: [],
      oldItems: [],
      loader: false,
      showmoviePopup: false,
      singleMovie: [],
    };
  },

  mounted() {
    this.favMovie = JSON.parse(sessionStorage.getItem("addeMovie")) || [];
  },

  methods: {
    openPopup() {
      console.log("Clicked", this.showPopup);
      this.showPopup = true;
    },
    closePopup() {
      this.showPopup = false;
    },

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
      //  console.log(index, this.newItems)
      //  this.oldItems = JSON.parse(sessionStorage.getItem("addeMovie")) || [];
      this.oldItems.push(this.newItems);
      this.favMovie = this.oldItems;
      console.log(this.oldItems, "");

      sessionStorage.setItem("addeMovie", JSON.stringify(this.oldItems));
    },
  },
};
</script>


<style scoped>
.titleDiv {
  width: 200px;
  height: 110px;
  border: solid 1px #ccc;
  text-align: center;
  padding-top: 70px;
  cursor: pointer;
  margin: 15px 15px 15px 25px;
  float: left;
}

.titleDiv p {
  text-align: center;
}

.modal {
  /*display: none;  Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 100px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0, 0, 0); /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 60%;
  overflow-y: scroll;
  height: 400px;
}
.modal_head {
  width: auto;
  border-bottom: solid 1px #ccc;
  height: 40px;
}
.modal_head > h5 {
  font-size: 16px;
}

/* The Close Button */
.exitcls {
  color: #aaaaaa;
  right: 275px;
  position: absolute;
  top: 110px;
  font-size: 30px;
  font-weight: bold;
  width: 30px;
}

.exitcls:hover,
.exitcls:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}
/*Modal css end*/

.container {
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}

/* search css start*/
div.form-group {
  padding-top: 30px;
  width: 100%;
  position: relative;
}

.example input[type="text"] {
  padding: 10px;
  font-size: 17px;
  /* border: 1px solid grey; */
  float: left;
  width: 90%;
  background: #f1f1f1;
  border: none;
}
.example button {
  float: right;
  width: 6%;
  padding: 10px;
  /* background: #2196F3; */
  color: #000;
  font-size: 17px;
  /* border: 1px solid grey; */
  border: none;
  right: 144px;
  cursor: pointer;
  position: absolute;
  outline: none;
  top: 30px;
}

.example button:hover,
.example button:active {
  /* background: #0b7dda; */
  border: none;
  outline: none;
}

.example::after {
  content: "";
  clear: both;
  display: table;
}

/* search css end*/

/*data fetch for home page start css*/
.btn-link {
  background-color: #5c940d;
  border: none;
  color: white;
  padding: 5px;
  border-radius: 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 13px;
  margin: 5px;
}

.btn-link:hover {
  background-color: #666;
}

.datafetch {
  width: 100%;
  float: left;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
.datafetch-movie {
  position: relative;
  top: 30px;
  float: left;
  width: 100%;
}

.fetch-movie-div {
  margin-left: 35px;
}
.fetch-movie-div-info {
  width: 150px;
  height: 300px;
  padding: 5px;
  margin: 15px 5px 5px 5px;
  float: left;
  border: dashed 1px #aaa;
}

.heightdiv {
  height: 265px;
}

.fetch-movie-div-info img {
  width: 150px;
  height: 200px;
}
.fetch-movie-div-info h5 {
  font-size: 14px;
  padding-top: 2px;
  margin: 0px;
}
.fetch-movie-div-info h5 span {
  font-weight: bold;
}
.fetch-movie-div-info a {
  font-size: 12px;
}
/*data fetch for home page end css*/

/* single MOvie info page start css*/
.info-page-move {
  width: 100%;
  float: left;
  margin-top: 20px;
}
.info-page {
  float: left;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
.info-page-img-divleft {
  width: 21%;
  float: left;
  position: relative;
  left: 35px;
  top: 38px;
}
.info-page-img-divleft img {
  width: 180px;
  height: 220px;
  float: left;
}
.info-page-img-divright {
  width: 68%;
  float: right;
  position: relative;
  left: 0px;
  top: 0px;
}
.info-page-img-divright h5 {
  padding: 3px;
  font-weight: bold;
  text-align: left;
  font-size: 20px;
  color: #1864ab;
  border-bottom: solid 2px #ccc;
}
.info-list {
  list-style-type: none;
  margin: 0px;
  padding: 0px;
  float: left;
  text-align: left;
  line-height: 25px;
}
.backbutton {
  font-size: 12px;
  background: black;
  color: white;
  display: block;
  padding: 10px;
  border-radius: 5px;
}
.info-list-div {
  float: left;
}
.backbutton:hover {
  text-decoration: underline;
  color: white;
}
.movieheading {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  font-size: 20px;
  color: rgb(0, 0, 0);
}
/* single MOvie info page end css*/
</style>