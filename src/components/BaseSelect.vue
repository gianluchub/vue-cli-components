<template>
  <select 
    :name="name" 
    :id="id"
    @change="$emit('change', $event.target.value)"    
    >
      <option 
        v-for="(option, index) in options"
        :key="index"
        :value="option"
        :selected="option === optionSelected"    
        >{{ option }}</option>
  </select>
</template>

<script>
export default {
    name: "BaseSelect",
    props: {
        name: {
            type: String
        },
        id: {
            type: String
        },
        options: {
            type: Array,
            default() {
               return ["normal", "fighting", "flying"]; 
            }
        },
        optionSelected: {
            type: String
        }
    }
}
</script>

<style>

</style>