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
            f7-searchbar(cancel-link='Cancelar', placeholder='Search pokemon', :clear='true')
            f7-list(media-list='')
              f7-list-item(title='Item 1', subtitle='Subtitle 1', text='Item 1 Text')
              f7-list-item(title='Item 1', subtitle='Subtitle 2', text='Item 2 Text', media="algoURL")

</template>

<script>
export default {
  name: 'app',
  mounted(){
    this.$http.get('http://pokeapi.co/api/v2/',{}, {}).then(res => {
      console.log(res);
    }).catch(err => {
      console.log(err);
    });
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App with Framework7 and Webpack'
    }
  }
}
</script>

<style lang="sass?indentedSyntax">
  /* Add your styles here */
</style>
