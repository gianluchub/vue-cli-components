<template>
  <option :value="value">{{ value }}</option>
</template>

<script>
export default {
    name: "BaseOption",
    props: {
        value: {
            type: String,
            required: true
        },
        selected: {
            type: Boolean,
            default() {
                return false;
            }
        }
    }
}
</script>

<style>

</style>