<template>
  <li>
      <a :href="url" target="_blank">{{ name }}</a>
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
            type: String
        },
        weight: {
            type: String
        },
    }
}
</script>

<style>

</style>