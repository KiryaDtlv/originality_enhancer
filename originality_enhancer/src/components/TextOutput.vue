<template>
  <v-textarea ref='textToCopy' readonly v-model="text"></v-textarea>
</template>

<script>
export default {
    props: [
        'text'
    ]
}
</script>

<style>

</style>