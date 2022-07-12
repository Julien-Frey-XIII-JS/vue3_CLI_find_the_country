<template>

  <div class="completed" v-if="show === true">
    Congratulations ! Try this other country..
  </div>

  <div>
      <button 
        class="change"
        @click="getRandomCountry"
      >
        New game
      </button>
  </div>

  <header class="header">
    Finds the country
  </header>

  <main class="main">

      <input 
        type="password"
        v-model="wordToFind"
        v-if="viewResponse === false"
      >

       <input 
        type="text"
        v-model="wordToFind"
        v-if="viewResponse === true"
      >

    <input 
      type="text"
      v-model="proposition"
      placeholder="Propose country"
    >

    <button @click="handleCheck">Check propose</button>

  </main>
 
  <footer>

    <div>
      TIPS ZONE ...
    </div>

    <div class="tipsZone">

      <div class="tip tip1" v-if="tips === 1 || tips === 2 || tips === 3 || tips > 3">
        The first word is {{ firstWord}}
      </div>

      <div class="tip tip2" v-if="tips === 2 || tips === 3 || tips > 3">
        The second word is {{ secondWord}}
      </div>

      <div class="tip tip3" v-if="tips === 3 || tips > 3">
        The third word is {{ thirdWord}}
      </div>

    </div>

 </footer>

</template>

<script setup>

import { ref } from 'vue';

  // ----- HOOKS -----
  let wordToFind = ref('');
  let proposition = ref('');
  let firstWord = ref('');
  let secondWord = ref('');
  let thirdWord = ref('');
  let tips = ref('');
  let show = ref(false);
  let viewResponse = ref(false)

  // Check proposition
  function handleCheck() {

    // Storage datas
    let word = wordToFind.value;
    let inputProposition = proposition.value;
    let tipsValue = tips.value;
    let showValue = show.value;

    if (word == inputProposition){

      console.log('yes');
      show.value = true;
    
      setTimeout(function(){

        getRandomCountry();

      }, 3000);
      

    }else{

      console.log('no');
      tips.value= tipsValue + 1 ;

    }

    proposition.value='';

  }

  // Get random country
  function getRandomCountry() {

    viewResponse.value = true;

    setTimeout(function(){
    
      viewResponse.value = false;

      // Fake datas
      const fakeDatas=
      [
        {name: 'Costa Rica', code: 'CR'}, 
        {name: 'Cote D\'Ivoire', code: 'CI'}, 
        {name: 'Croatia', code: 'HR'}, 
        {name: 'Cuba', code: 'CU'}, 
        {name: 'Cyprus', code: 'CY'}, 
        {name: 'Czech Republic', code: 'CZ'}, 
      ] ;

      // Choose random country
      let randomCountry = fakeDatas[Math.floor(Math.random() * fakeDatas.length)];
      let countryName = randomCountry.name.toLowerCase();

      // Split random country name
      let firstWordIs = countryName.substring(0,1);
      let secondWordIs = countryName.substring(1,2);
      let thirdWordIs = countryName.substring(2,3);
      
      // Set datas
      wordToFind.value=countryName;
      firstWord.value=firstWordIs;
      secondWord.value=secondWordIs;
      thirdWord.value=thirdWordIs;
      tips.value=0;
      show.value = false;

    }, 3000);
  }

  getRandomCountry();

</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Fascinate&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Fascinate&family=League+Gothic&display=swap');

  #app{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradient 15s ease infinite;
    height: 100vh;
  }
  
  .main{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .header{
    font-size: 2em;
    font-weight: bold;
    margin-bottom: 1em;
    font-family: 'Fascinate', sans-serif;
  }

  .main{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .tipsZone{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-bottom: 1em;
    font-family: 'League Gothic', sans-serif;
  }

  .tip{
    font-size: 2em;
    font-weight: bold;
    margin-bottom: 0.6em;
  }

  button{
    font-size: 1em;
    font-weight: bold;
    background-color: #23a6d5;
    margin-top: 0.8em;
    border-radius: 8px;
    width: 220px;
    height: 30px;
  }

  input{
    font-size: 1em;
    font-weight: bold;
    margin-top: 0.3em;
    text-align: center;
    border-radius: 8px;
    background-color:rgb(202, 196, 196);
  }

  footer{
    position: fixed;
    bottom: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-top: 1em;
  }
  
  .change{
    font-size: 0.7em;
    font-weight: bold;
    background-color: #23a6d5;
    margin-top: 0.8em;
    width: 60px;
    height: 60px;
    border-radius: 30px;
  }

  .completed{
    font-size: 1.5em;
    font-weight: bold;
    margin-bottom: 1em;
    font-family: 'Fascinate', sans-serif;
  }

  @keyframes gradient {
	0% {
		background-position: 0% 50%;
	}
	50% {
		background-position: 100% 50%;
	}
	100% {
		background-position: 0% 50%;
	}
}

</style>

