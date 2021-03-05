<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <ul>
      <li>Elenco puntato senza stile</li>
    </ul>  
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <Title message="I pokemon di Classe #22" />

    <FormCustom 
      title="Cerca un Pokemon" 
      @sendForm="searchPokemon" 
      @sendTypeSelected="sendTypeSelected"
    />

    <FormCustom 
      title="Cerca per tipologia" 
      @sendForm="searchType" 
      @sendTypeSelected="sendTypeSelected"
    />
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
        // console.log(response.data);
        // https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg

        // console.log("URL: " + response.data.results[0].url);
        // console.log(response.data.results[0].url.split("/"));

        // this.pokemons = response.data.results;

        response.data.results.forEach(
          (element) => {
            const idArray = element.url.split("/");
            const id = idArray[idArray.length - 2];

            this.pokemons.push(
              {
                ...element,
                img: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${id}.svg`
              }
            );

          }
        );

        console.log(this.pokemons);
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
            weight: response.data.weight,
            img: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${response.data.id}.svg`
          }  
        ];
      });
    },
    searchType: function(text) {
      this.axios
      .get(`${this.base_url}/type/${text}`)
      .then( (response) => {
        // console.log("Type Search");
        // console.log(response.data.pokemon);
  

        this.pokemons = response.data.pokemon.map(
          (element) => {
            // console.log(element);
            const idArray = element.pokemon.url.split("/");
            const id = idArray[idArray.length - 2];

            return {
              "name": element.pokemon.name, 
              "url": element.pokemon.url,
              "img": `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${id}.svg`
            }
          }
        );
      });
    },
    sendTypeSelected: function(text){
      console.log("Opzione selezionata arrivata fino ad App: " + text);
      this.searchType(text);
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
  padding: 0;
}
</style>
