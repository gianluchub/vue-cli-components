<template>
  <input v-if="type === 'submit'"
    :type="type"
    :name="name"
    :id="id"
    :value="value"
    @click="$emit('click')"
    >

    <input v-else
    :type="type"
    :name="name"
    :id="id"
    :placeholder="placeholder"
    :value="value"
    @input="$emit('input', $event.target.value)"
    >
</template>

<script>
export default {
    name: "BaseInput",
    props: {
        type: {
            type: String,
            required: true
        },
        name: {
            type: String,
        },
        id: {
            type: String
        },
        value: {
            type: String
        },
        placeholder: {
            type: String
        }
    }
}
</script>

<style>

</style>