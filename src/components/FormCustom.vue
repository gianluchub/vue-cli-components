<template>
   <div class="form-container">
        <h2>{{ title }}</h2>
        <form @submit.prevent>
            <!-- <input type="text" v-model="searchText"> -->
            <BaseInput 
                type="text"
                placeholder="Scrivi qui la tua ricerca"
                :value="searchText"
                @input="searchText = $event"
            />
            <!-- <input type="submit" value="Cerca" @click="sendSearch"> -->

            <BaseSelect
                :optionSelected="typeSelected"
                @change="sendType($event)"
            />

            <BaseInput
                type="submit"
                value="Cerca"
                @click="sendSearch"     
            />
        </form>
   </div>
</template>

<script>
import BaseInput from "./BaseInput.vue";
import BaseSelect from "./BaseSelect.vue";

export default {
    name: "FormCustom",
    props: [ "title" ],
    components: {
        BaseInput,
        BaseSelect
    },
    data() {
        return {
            searchText: "",
            typeSelected: ""
        }
    },
    methods: {
        sendSearch: function() {
            // console.log(this.searchText);
            // var array = [1, "pippo"];
            this.$emit('sendForm', this.searchText);
        },
        sendType: function(text) {
            console.log(text);
            this.typeSelected = text;
            this.$emit("sendTypeSelected", this.typeSelected);
        }
    }
}
</script>

<style lang="scss">
    @import '../scss/_variables.scss'; 

    .form-container {
        padding: 15px 0;
        background-color: $green;
        margin: 15px 0;
    }
</style>