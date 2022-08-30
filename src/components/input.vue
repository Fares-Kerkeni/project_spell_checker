<template>
  
   
<!-- the text correction--> 
<div class="all">
       <div>Enter the text you want to correct.</div>
    <input type="text" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"/>
    <input type="submit" @click="submit">
    
    <div class="words">
        <div class="error_word" v-for="post in  splits " v-bind:key="post.id" >
            {{post}}
        </div> 
    </div>
    <div>
        {{errors_copie}}
    </div>
</div>
 
    
    
</template>

<script>
/* eslint-disable no-mixed-spaces-and-tabs */
import axios from 'axios'
export default {
    name: 'input_user',
    props:{
        modelValue: String
    },
    data(){
        return{
            test: '',
            comp: 0,
            splits:[],
            
        }
    },
    created(){
      axios.get()
    },
    methods:{
        submit: function(){
            //stocker le text utilisateur
            this.test+=this.modelValue
            //tranformation en tableau
            this.splits = this.test.split(" ");
            console.log()
            this.api()
            
            
        },
        // change_text: function(texte){
        //     var splits = texte.split(" ", 3);
        //     console.log("re")
        //     return splits
        // },
        api: function(){
            const axios = require("axios");
            const options = {
              method: 'POST',
              url: 'https://jspell-checker.p.rapidapi.com/check',
              headers: {
                'content-type': 'application/json',
                'X-RapidAPI-Key': 'b99b6429b8msh5b66ff41fd65591p1c52f0jsn03117ac8e6dc',
                'X-RapidAPI-Host': 'jspell-checker.p.rapidapi.com'
              },
              data: '{"language":"frFR","fieldvalues":"1","config":{"forceUpperCase":false,"ignoreIrregularCaps":false,"ignoreFirstCaps":true,"ignoreNumbers":true,"ignoreUpper":false,"ignoreDouble":false,"ignoreWordsWithNumbers":true}}'
            };
            //modification de la valeur de data

            options.data=options.data.replace('1', this.test);
            
            axios.request(options).then(function (response) {
                //const suggestions=response.data.elements[0].errors[0].suggestions
                //recuperation erreur utilisateur
                const errors = response.data.elements[0].errors
                var copie = [];
                
                errors.forEach(element => copie.push(element.word));
                // errors.forEach(element => console.log(element.suggestions));
                console.log(copie)
                // console.log(errors)

                // console.log(suggestions)
            }).catch(function (error) {
	            
                console.error(error);
                
            });
           
        }
    }
};

</script>

<style lang="scss">
.all{
    display: flex;
   
    align-items: center;
    justify-content: start;
    flex-direction: column;
   
    .words{
        width: 500px;
        height: 500px;
        border: solid black;
        margin: 50px;
        
        flex-direction: row;
    .error_word{
       margin: 0;
      
    
    }
}
   
}


</style>