<template>
  <v-textarea :rules="[v => !!v || 'Поле является обязательным']" v-model="currentText"></v-textarea>
</template>

<script>

export default {
    props: ['text'],
    data(){
        return {
            currentText: this.text
        }
    },
    watch: {
        currentText() {
            console.log(this.currentText)
            this.$emit('update', this.currentText)
        }
    }

}
</script>

<style>

</style>