<template lang="pug">
  li.artist
    h2: a(:href="artist.url", target="_blank") {{ artist.name }}
    img(:src="getImageUrl(artist.image)")
</template>

<script>
export default {
  name: "artist",
  props: ["artist"],
  methods: {
    getImageUrl(imageList) {
      for (const image of imageList) {
        if (image.size === "large") {
          return image["#text"];
        }
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang='stylus' scoped>
li.artist
  display block
  margin 10px 0
</style>
