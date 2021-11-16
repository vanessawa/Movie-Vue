<template>
  <header>
    <h1>Movie Finder</h1>
    <p>Search your movie</p>
    <input
      id="input-title"
      type="text"
      placeholder="Title"
      v-model="title"
      @keypress.enter="onClick"
    />
    <input
      id="input-year"
      type="text"
      placeholder="Year"
      v-model="year"
      @keypress.enter="onClick"
    />
    <button id="search-btn" @click="onClick">Search</button>
  </header>
  <div id="result" v-if="result">
    <h3>Result</h3>

    <p id="result-title">Title: {{ result.Title }}</p>

    <p id="result-year">Year: {{ result.Year }}</p>

    <p id="result-actors">Actors: {{ result.Actors }}</p>

    <p id="result-genre">Genre: {{ result.Genre }}</p>

    <p id="result-production">Production: {{ result.Production }}</p>

    <p id="result-director">Director: {{ result.Director }}</p>

    <p id="result-country">Country: {{ result.Country }}</p>

    <p id="result-awards">Awards: {{ result.Awards }}</p>

    <p id="result-plot">Plot: {{ result.Plot }}</p>

    <img v-bind:src="result.Poster" />
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      title: "",
      year: "",
      result: null,
    };
  },
  methods: {
    onClick() {
      fetch(
        "https://www.omdbapi.com/?apikey=167eb644&t=" +
          this.title +
          "&y=" +
          this.year
      )
        .then((response) => response.json())
        .then((data) => (this.result = data));
      fetch("http://img.omdbapi.com/?apikey=167eb644")
        .then((response) => response.json())
        .then((data) => (this.result = data));
    },
  },
};
</script>

<style lang="scss">
header {
  background-image: url("https://www.decopoint.at/media/image/product/94792/md/filmstreifen-kunststoff-140x19cm-art_nr7344641.jpg");
  background-size: cover;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: 400px;
}
</style>
