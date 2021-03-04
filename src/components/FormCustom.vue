<template>
   <div class="form-container">
        <h2>{{ title }}</h2>
        <form @submit.prevent>
            <input type="text" v-model="searchText">
            <input type="submit" value="Cerca" @click="sendSearch">
        </form>
   </div>
</template>

<script>
export default {
    name: "FormCustom",
    props: [ "title" ],
    data() {
        return {
            searchText: ""
        }
    },
    methods: {
        sendSearch: function() {
            // console.log(this.searchText);
            // var array = [1, "pippo"];
            this.$emit('sendForm', this.searchText);
        }
    }
}
</script>

<style>
    .form-container {
        background-color: lightblue;;
        margin-bottom: 30px;
    }
</style>