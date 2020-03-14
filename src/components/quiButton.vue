<template>
  <div @click="alertMsg">
    {{msg}}
  </div>
</template>

<script>
    export default {
        name: "quiButton",
        props: {
            msg: {
                type: String,
                default: '',
            },
        },
        methods: {
            alertMsg() {
                this.$emit('btnClickEvent', true);
                // console.log(222)
            },
        },
    }
</script>

<style scoped>

</style>
