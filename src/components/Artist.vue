<template lang="pug">
  li.artist
    h2: a(:href="artist.url" target=_blank) {{ artist.name }}
    img(:src="artist.image[2]['#text']")
</template>

<script>
export default {
 name: 'artist',
 props: ['artist']
}
</script>

<style lang="stylus">
    ul
        display flex
        flex-wrap wrap
        justify-content center
    li.artist
        margin 30px;
    img
        width 280px
        border-radius 10px
</style>
