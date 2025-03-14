<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :movies = "movies.length" :favourite = "movies.filter(e => e.favourite).length"/>
      <div class="search-panel">
        <SearchPanel @onSearch = "updateTermHandler"/>
        <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter"/>
      </div>
      <MovieList :moviesData = "onFilterHandler(onSearchHandler(movies, term), filter)" @onToggle="onToggle" @removeItem = "onRemove"/>  
      <MovieAddForm @createMovie="createMovie"/>
    </div>
  </div>
</template>

<script>
import AppInfo from "./components/app-info/AppInfo.vue"
import SearchPanel from "./components/search-panel/SearchPanel.vue"
import AppFilter from "./components/app-filter/AppFilter.vue"
import MovieList from "./components/movie-list/MovieList.vue"
import MovieAddForm from "./components/movie-add-form/MovieAddForm.vue"

  export default {
    components : {
      AppInfo,
      SearchPanel,
      AppFilter,
      MovieList,
      MovieAddForm,
    },
    data() {
        return {
            movies: JSON.parse(localStorage.getItem("movies")) || [
                {                  
                    id : 1,
                    name: "Omar",
                    viewers: 811,
                    favourite: false,
                    like: true
                },
                {
                    id : 2,
                    name: "Justice League",
                    viewers: 411,
                    favourite: false,
                    like: false
                },
                {
                    id : 3,
                    name: "Ertugul",
                    viewers: 711,
                    favourite: true,
                    like: false
                }
            ],
            term: "",
            filter: "",
        }
    },
    methods : {
      createMovie(item){
        this.movies.push(item)
        localStorage.setItem("movies", JSON.stringify(this.movies))          
      },
      onToggle({id, prop}){
        localStorage.setItem("movies", JSON.stringify(this.movies.map(e=>{          
          if(e.id===id){     
            e[prop] = !e[prop]
          }
          return e      
        })))        
      },
      onRemove(id){
        localStorage.setItem("movies", JSON.stringify(this.movies = this.movies.filter(e=>e.id !== id)))
        this.movies.length === 0 && localStorage.removeItem("movies")
      },
      onSearchHandler(arr, term){
        // if(term.length === 0){
        //   return arr
        // }
                  
        return arr.filter(e=>e.name.toLowerCase().includes(term.toLowerCase()))        
      },
      onFilterHandler(arr, filter){
        switch (filter) {
          case "popular":
            return arr.filter(e=>e.like)

          case "mostViewers":
            return arr.filter(e=>e.viewers>500)

          default:
            return arr
        }             
      },
      updateTermHandler(term){
        this.term = term
      },
      updateFilterHandler(filter){
        this.filter = filter
      }
    }
  }
</script>


<style>
.app{
  height: 100vh;
  color: #000;
}
.content{
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel{
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcf5faf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>