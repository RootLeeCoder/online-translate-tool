<template>
  <div id="app">
    <h1>Online Translate</h1>
    <h5 class="text-muted">Simple / Easy / Elegant</h5>
    <translateForm v-on:formSubmit="translateText"></translateForm>
    <br><br>
    <translateOutput v-text="translatedText" style="color: red; font-size: 20px; font-family: '微软雅黑'"></translateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'

export default {
  name: 'app',
  data: function(){
    return {
      translatedText: ""
    }
  },
  components: {
    TranslateForm, TranslateOutput
  },
  methods: {
    translateText: function(text, language) {
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170721T082515Z.54cf3dc583f679db.f4a96182281281d8b5dfe24b4e88298e2133f219&lang='+language+'&text='+text)
        .then((response)=>{
          this.translatedText = response.body.text[0];
        })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
