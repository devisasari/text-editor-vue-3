<script setup>
import { ref } from 'vue'
import { saveAs } from 'file-saver'

const text = ref('')
const openFile = () => {
  const input = document.createElement('input')
  input.type = 'file'
  input.onchange = e => {
    const file = e.target.files[0]
    const reader = new FileReader()
    reader.onload = e => {
      text.value = e.target.result
    }
    reader.readAsText(file)
  }
  input.click()
}

const saveFile = () => {
  const blob = new Blob([text.value], { type: 'text/plain;charset=utf-8' })
  saveAs(blob, 'text.txt')
}

const countWords = () => {
  const words = text.value.split(' ')
  alert(`There are ${words.length} words in the text.`)
}

const countCharacters = () => {
  const characters = text.value.split('')
  alert(`There are ${characters.length} characters in the text.`)
}
</script>

<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <h1>Text Editor</h1>
          <div class="form-group">
            <textarea class="form-control" rows="10" placeholder="Type here or open .txt file" v-model="text"></textarea>
          </div>
          <div class="form-group">
            <button class="btn btn-primary" @click="openFile">Open</button>
            <button class="btn btn-primary" @click="saveFile">Save</button>
            <button class="btn btn-primary" @click="countWords">Count Words</button>
            <button class="btn btn-primary" @click="countCharacters">Count Characters</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  margin-top: 50px;
}

textarea {
  width: 100%;
  height: 300px;
  resize: true;
}
</style>