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
            f7-searchbar(cancel-link='Cancelar', placeholder='Search pokemon', :clear='true', v-model="search")
            f7-preloader.center(v-if="! pokemons")
            f7-list(media-list)
              f7-list-item(v-for="(pokemon , index) in pokemons", 
                :title='name(pokemon.name)', 
                subtitle='Subtitle 1', 
                :text='pokemon.url', 
                :media='image(index+1)')

</template>

<script>
export default {
  name: 'app',
  mounted(){
    this.$http.get('http://pokeapi.co/api/v2/pokemon/?limit=151&offset=0',{}, {}).then(res => {
      this.pokemons = res.body.results;
      // console.log(this.pokemons);
      console.log(res.body.results);
    }).catch(err => {
      console.log(err);
    });
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App with Framework7 and Webpack',
      search: '',
      pokemons: {}
    }
  },
  methods: {
    image(id) {
      return '<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+id+'.png">';
    },
    name(name) {
      return name.charAt(0).toUpperCase() + name.substr(1).toLowerCase();
    }
  }
}
</script>

<style lang="sass?indentedSyntax">
  /* Add your styles here */
</style>
