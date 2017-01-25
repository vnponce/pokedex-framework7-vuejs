<template lang="jade">
  div#app
    f7-views(navbar-through='')
      f7-view(main='', url='/', :dynamic-navbar='true')
        f7-navbar
          f7-nav-left
          f7-nav-center(sliding='') Home
          f7-nav-right
        f7-pages#pages
          f7-page.navbar-fixed
            f7-searchbar(cancel-link='Cancelar', placeholder='Search pokemon', :clear='true', v-model="search", @keyup.enter="filterPokemons")
            f7-preloader.center(v-if="!pokemons")
            f7-list(media-list)
              f7-list-item(v-for="(pokemon , index) in filteredPokemons", 
                :title='name(pokemon.name)', 
                :subtitle='pokemon.url', 
                text='', 
                :media='image(pokemon.url)',
                :link="details(pokemon.url)")

</template>

<script>
export default {
  name: 'app',
  mounted(){
    this.$http.get('http://pokeapi.co/api/v2/pokemon/?limit=151&offset=0',{}, {}).then(res => {
      this.pokemons = res.body.results;
      this.filteredPokemons = this.pokemons;
      // console.log(this.pokemons);
      console.log(res.body.results);
    }).catch(err => {
      console.log(err);
    });
  },
  data () {
    return {
      msg: 'Welcome to Your Pokedex App with Vue.js, Framework7 and Webpack',
      search: '',
      pokemons: {},
      filteredPokemons: {}
    }
  },
  methods: {
    image(url) {
      let id = this.getId(url);
      return '<img class="lazy" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+id+'.png">';
    },
    name(name) {
      return name.charAt(0).toUpperCase() + name.substr(1).toLowerCase();
    },
    filterPokemons(){
      console.log('change');
      if(this.search !== ''){
        this.filteredPokemons =  this.filteredPokemons.filter(pokemon => {
          if( pokemon.name == this.search ){
            return pokemon;
          }
        });
      }
      this.filteredPokemons = this.pokemons;
    },
    getId(url){
      let id = url.match(/http:\/\/pokeapi.co\/api\/v2\/pokemon\/(\d+)\//);
      return id[1];
    },
    details(url){
      return '/pokemon/' + this.getId(url);
    }
  },
}
</script>

<style lang="sass?indentedSyntax">
  /* Add your styles here */
</style>
