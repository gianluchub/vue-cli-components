<template>
  <li>
      <a :href="url" target="_blank">
          <h4>{{ name }}</h4>
          <img :src="img" :alt="name">
        </a>
      <p v-if="height"><strong>Altezza: </strong>{{ height }}</p>
      <p v-if="weight"><strong>Peso: </strong>{{ weight }}</p>
  </li>
</template>

<script>
export default {
    name: "Card",
    // props: ["name", "url"]
    props: {
        name: {
            type: String,
            required: true
        },
        url: {
            type: String,
            required: true
        },
        height: {
            type: Number
        },
        weight: {
            type: Number
        },
        img: {
            type: String
        }
    }
}
</script>

<style lang="scss" scoped>
    @import '../scss/_variables.scss';    

    li {
        width: calc(100% / 4 - 10px);
        margin: 5px;
        text-align: center;
        background-color: $blue;

        a {
            text-decoration: none;
            color: darken($blue, 50%);
        }
    }
    img {
        width: 60%;
        margin-bottom: 1.33em;
    }
</style>