<template lang="pug">
  #app
    img(src='https://maycolur7.github.io/TopMusicsApp/dist/assets/logo.png')
    h1 PlatziMusic
    label(for="selector") Elija un país
    br
    select(v-model="selectedCountry" id="selector")
      option(v-for="country in countries" :value="country.value") {{ country.name }}
    spinner(v-show="loading")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" :key="artist.mbid")

</template>

<script>
import getArtists  from './api/index'
import Artist from './components/Artist'
import spinner from './components/spinner'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { name: 'Argentina', value: 'argentina' },
        { name: 'Colombia', value: 'colombia' },
        { name: 'Velezuela', value: 'venezuela' },
        { name: 'España', value: 'spain' },
        { name: 'Alemania', value: 'germany' }
      ],
      selectedCountry: 'venezuela',
      loading: true
    }
  },
  components: {
    Artist,
    spinner
  },
  methods: {
    refreshArtist() {
       const self = this;
       self.loading = true
       self.artist = []
      getArtists(this.selectedCountry)
        .then( function(artist) {
          self.artists = artist;
          self.loading = false
        })
    }
  },
  mounted() {
    this.refreshArtist();
  },
  watch: {
    selectedCountry() {
      this.refreshArtist();
    }
  }
}
</script>

<style lang="stylus">
  body
    background-color #42b983
    font-family: 'Supermercado One', cursive
  #app
    margin 0 30px
    font-family 'Avenir', Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color #2c3e50
    margin-top 60px
    background #f7f9f8
    border-radius 10px;

  h1, h2
    font-weight normal

  ul
    list-style-type none
    padding 0

  li
    display inline-block
    margin 0 10px

  a
    color #42b983
  select 
    margin 10px
</style>
