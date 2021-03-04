<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <Title message="I pokemon di Classe #22" />

    <FormCustom title="Cerca un Pokemon" @sendForm="searchPokemon" />

    <FormCustom title="Cerca per tipologia" @sendForm="searchType" />
    <!-- <ul>
      <li v-for="(pokemon, index) in pokemons" :key="index">
        <a :href="pokemon.url" target="_blank">{{ pokemon.name }}</a>
      </li>
    </ul> -->
    <Cards :cards="pokemons" />
    <!-- <Cards :cards="players" className="cards" /> -->
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import Title from "./components/Title.vue";
import Cards from "./views/Cards.vue";
import FormCustom from "./components/FormCustom.vue";

export default {
  name: "App",
  components: {
    // HelloWorld
    Title,
    Cards,
    FormCustom
  },
  data() {
    return {
      pokemons: [],
      players: [
        {
          "name": "Roberto Baggio"
        },
        {
          "name": "Francesco Totti",
          "url": "url2"  
        },
      ]
    }
  },
  mounted() {
    this.axios
      .get(`${this.base_url}/pokemon`)
      .then( (response) => {
        console.log(response.data);

        this.pokemons = response.data.results;
      });
  },
  methods: {
    searchPokemon: function(text) {
      console.log(text);

      this.axios
      .get(`${this.base_url}/pokemon/${text}`)
      .then( (response) => {
        console.log(response.data);

        this.pokemons = [
          {
            name: response.data.name,
            url: `${this.base_url}/pokemon/${text}`,
            height: response.data.height,
            weight: response.data.weight
          }  
        ];
      });
    },
    searchType: function(text) {
      this.axios
      .get(`${this.base_url}/type/${text}`)
      .then( (response) => {
        // console.log("Type Search");
        console.log(response.data.pokemon);

        this.pokemons = response.data.pokemon.map(
          (element) => {
            // console.log(element);

            return {
              "name": element.pokemon.name, 
              "url": element.pokemon.url
            }
          }
        );
      });
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul{
  list-style: none;
  margin: 0;
}
</style>
