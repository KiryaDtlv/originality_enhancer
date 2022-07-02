<template>
  <v-card>
      <v-card-text>
        <text-input :text="currentText" @update="(v) => currentText = v" />
            <!-- <text-output :text="originalityText" /> -->
            <v-textarea ref='textToCopy' readonly v-model="originalityText"></v-textarea>
        </v-card-text>
        <v-card-actions>
            <!-- <my-btn :title="'Повысить оригинальность'" ></my-btn> -->
            <v-btn color="primary" :disabled="currentText ? false : true" @click="getOriginality(currentText)">Повысить оригинальность</v-btn>
            <v-btn :disabled="originalityText ? false : true" color="green" @click="copyText()">Копировать</v-btn>
        </v-card-actions>
       
  </v-card>
</template>

<script>
import TextInput from '../components/TextInput.vue'
import TextOutput from '../components/TextOutput.vue'
import MyBtn from '../components/MyBtn.vue'
export default {
  components: { TextInput,  MyBtn, TextOutput },
    data(){
        return {
            currentText: undefined,
            ruKeysEnValues: {'у': 'y', 'е': 'e', 'а': 'a', 'о': 'o', 'р': 'p','с': 'c', 'А': 'A', 'Р': 'P', 'Е': 'E', 'О': 'O', 'С': 'C', 'Н': 'H', 'К': 'K'},
            originalityText: undefined
        }
    },
    watch: {
    },
    methods: {
        getRandomInt(max) {
            return Math.floor(Math.random() * max);
        },
        getIndices(splittedText){
            let indices = [] 

            for (let key of Object.keys(this.ruKeysEnValues)){
                
                let firstPosition = splittedText.indexOf(key)

                while (firstPosition != -1 && !indices.includes(firstPosition)){
                    indices.push(firstPosition)
                    console.log(firstPosition)
                    firstPosition = splittedText.indexOf(key, firstPosition)
                }
            }
            return indices
        },
        shuffle(array) {
            let currentIndex = array.length, randomIndex;

            // While there remain elements to shuffle.
            while (currentIndex != 0) {

                // Pick a remaining element.
                randomIndex = Math.floor(Math.random() * currentIndex);
                currentIndex--;

                // And swap it with the current element.
                [array[currentIndex], array[randomIndex]] = [
                array[randomIndex], array[currentIndex]];
            }

            return array;
        },
        getOriginality(text){
            let splittedText = text.split('')
            let counter = 0
            let currentIndices = this.getIndices(splittedText)
            // console.log('dl: ', currentIndices.length)
            let randInt = this.getRandomInt(currentIndices.length)
            let max_letters = Math.min(randInt, currentIndices.length)
            // console.log(currentIndices)
            // console.log('max: ', max_letters)
            while (counter < max_letters){
                // console.log('Im here')
                let index = this.shuffle(currentIndices)[0]
                // console.log(splittedText[index], index)
                // console.log(Object.keys(this.ruKeysEnValues).includes(splittedText[index]))
                if (!Object.keys(this.ruKeysEnValues).includes(splittedText[index])){
                    currentIndices.splice(0, 1);
                    continue
                }
                // console.log(index)
                // console.log(splittedText[index].charCodeAt(0), this.ruKeysEnValues[splittedText[index]].charCodeAt(0))
                // console.log('before: ', splittedText[index].charCodeAt(0) == this.ruKeysEnValues[splittedText[index].charCodeAt(0)])
                splittedText[index] = this.ruKeysEnValues[splittedText[index]]
                // if (index > -1) { // only splice array when item is found
                currentIndices.splice(0, 1); // 2nd parameter means remove one item only
                // }
                // console.log('after: ', splittedText[index].charCodeAt(0) == this.ruKeysEnValues[splittedText[index].charCodeAt(0)])
                // console.log(splittedText[index].charCodeAt(0))
                // console.log(splittedText[index].charCodeAt(0), this.ruKeysEnValues[splittedText[index]].charCodeAt(0))
                counter++
            }
            
            this.originalityText = splittedText.join('')
            // console.log(splittedText)
        },
        copyText () {
          let textToCopy = this.$refs.textToCopy.$el.querySelector('textarea')
          textToCopy.select()
          document.execCommand("copy");
        }
    }
}
</script>

<style>

</style>