<template lang="jade">
  f7-page(hide-bars-on-scroll='')
    f7-navbar(back-link='Back', :title='name', sliding='')
    f7-block(v-if="pokemon.types")
      f7-card(:title="title", :content='content', footer='Card Footer')
      p Tipo:
      f7-chip(v-for="type in pokemon.types", :text='type.type.name')
</template>

<script>
export default {
  created(){
    window.f7.showPreloader();
    let url = 'http://pokeapi.co/api/v2/pokemon/'+this.$route.params.id;
    this.$http.get(url,{}, {}).then(res => {
      this.pokemon = res.body;
      this.name = this.pokemon.name;
      window.f7.hidePreloader();
    }).catch(err => {
      console.log(err);
    });

/* Evolutions API does not work correctly... or maybe I don't know how use it
    window.f7.showPreloader();
    let url = 'http://pokeapi.co/api/v2/evolution-c/'+this.$route.params.id;
    this.$http.get(url,{}, {}).then(res => {
      this.evolutions = res.body;
      window.f7.hidePreloader();
      console.log(this.evolutions);
    }).catch(err => {
      console.log(err);
    });
*/
  },
  name: 'pokemonDetails',
  data () {
    return {
      id: this.$route.params.id,
      pokemon: {},
      name: ''
      // evolutions: {}
    }
  },
  computed: {
      title(){
        return 'This is ' + this.pokemon.name +' page!';
      },
      content(){
        return '<div valign="bottom" class="card-header color-black no-border">'+this.pokemon.name+'</div><div class="img" style="background-image:url('+ this.url_image +')" ></div><p>Level: '+this.pokemon.base_experience+'</p>';
      },
      url_image(){
        return 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+this.id+'.png';
      }
    }
}
</script>

<style lang="sass?indentedSyntax">
  // Add your styles here.
  // See the following link for info on indented syntax:
  // http://sass-lang.com/documentation/file.INDENTED_SYNTAX.html

  .red
    span
      color: red

  .cursive
    span
      font-style: italic

  .img
    background-repeat: no-repeat
    width: 100%
    height: 15vh
</style>
