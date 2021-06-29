<template>
        <div class="container">

          <div>
            <div class="input-container">
              <h3>2. Edit Legend </h3>              
              <p>Situation 1</p><input v-model="message1" type="text">
              <p>Situation 2</p><input v-model="message2" type="text">
              <p>Situation 3</p><input v-model="message3" type="text">
              <p>Situation 4</p><input v-model="message4" type="text">
            </div>
          </div>

          <div class="box" id="my-node">

            <button   class="grow grid" v-on:click="selectHand" v-for="item in this.fullDeck" :key="item">{{item}} </button>

            <div class="title-choice-container">              
              <button v-on:click="selectHand" class="btn-choice"></button><p class="title-choice">{{ message1 }}</p>
              <button v-on:click="selectHand" class="btn-choice"></button><p class="title-choice">{{ message2 }}</p>
              <button v-on:click="selectHand" class="btn-choice"></button><p class="title-choice">{{ message3 }}</p>
              <button v-on:click="selectHand" class="btn-choice"></button><p class="title-choice">{{ message4 }}</p>
            </div>
          </div>
          
        </div>
</template>



<script>
export default {
data() {
        
        const firstCard = ["A", "K", "Q","J","T","9","8","7","6","5","4","3","2"]
        const secondCard = ["A","K","Q","J","T","9","8","7","6","5","4","3","2"]
        const fullDeck = []

        return {
            firstCard,
            secondCard,
            fullDeck,
            message1:"Change Situation",   
            message2:"Change Situation",   
            message3:"Change Situation",
            message4:"Change Situation",
        }
    }, 
   
    mounted() {
        this.generateDeck();

        // this is the default hsl color if user doesnt pick a color
        this.$store.hue = 50
        this.$store.saturation= 100
        this.$store.luminosity= 50
        this.$store.alpha= 1


    },
    methods: {
        generateDeck() {

            for (const secondCard in this.firstCard) {
            for (const firstCard in this.secondCard) { 
            const pairGenerated = this.secondCard[firstCard] + this.firstCard[secondCard] 
                
            //    PUSHING SUITED PAIRS TO THE GRID

            // The reason for this mess ⬇️⬇️⬇️ is the only way I came up with to have all suiteds like; AKs AQs and not like: KAs QAs
            // .split("") to divide the firstHand from secondHand with ","
            // .reverse() to change the position of the elments separated with comas
            // .join("") to agroup again the elements.

            if (pairGenerated =="23"
            || pairGenerated == "24"||pairGenerated == "25"||pairGenerated == "26"||pairGenerated == "27"||pairGenerated == "28"||pairGenerated == "29"||pairGenerated == "2T"||pairGenerated == "2J"||pairGenerated == "2Q"||pairGenerated == "2K"||pairGenerated == "2A"
            || pairGenerated == "34"||pairGenerated == "35"||pairGenerated == "36"||pairGenerated == "37"||pairGenerated == "38"||pairGenerated == "39"||pairGenerated == "3T"||pairGenerated == "3J"||pairGenerated == "3Q"||pairGenerated == "3K"||pairGenerated == "3A" 
            || pairGenerated == "45"||pairGenerated == "46"||pairGenerated == "47"||pairGenerated == "48"||pairGenerated == "49"||pairGenerated == "4T"||pairGenerated == "4J"||pairGenerated == "4Q"||pairGenerated == "4K"||pairGenerated == "4A"
            || pairGenerated == "56"||pairGenerated == "57"||pairGenerated == "58"||pairGenerated == "59"||pairGenerated == "5T"||pairGenerated == "5J"||pairGenerated == "5Q"||pairGenerated == "5K"||pairGenerated == "5A"           
            || pairGenerated == "67"||pairGenerated == "68"||pairGenerated == "69"||pairGenerated == "6T"||pairGenerated == "6J"||pairGenerated == "6Q"||pairGenerated == "6K"||pairGenerated == "6A"           
            || pairGenerated == "78"||pairGenerated == "79"||pairGenerated == "7T"||pairGenerated == "7J"||pairGenerated == "7Q"||pairGenerated == "7K"||pairGenerated == "7A"           
            || pairGenerated == "89"||pairGenerated == "8T"||pairGenerated == "8J"||pairGenerated == "8Q"||pairGenerated == "8K"||pairGenerated == "8A"          
            || pairGenerated == "9T"||pairGenerated == "9J"||pairGenerated == "9Q"||pairGenerated == "9K"||pairGenerated == "9A"           
            || pairGenerated == "TJ"||pairGenerated == "TQ"||pairGenerated == "TK"||pairGenerated == "TA"           
            || pairGenerated == "JQ"||pairGenerated == "JK"||pairGenerated == "JA"           
            || pairGenerated == "QK"||pairGenerated == "QA"           
            || pairGenerated == "KA"){

            this.fullDeck.push(`${pairGenerated.split("").reverse().join("")}`+"s")
  
                         
            //    PUSHING POCKETS PAIRS TO THE GRID            
            }else if(pairGenerated == "22" ||pairGenerated == "33" ||pairGenerated == "44" ||pairGenerated == "55" ||pairGenerated == "66"
            || pairGenerated == "77" ||pairGenerated == "88"||pairGenerated == "99"||pairGenerated == "TT"||pairGenerated == "JJ"
            ||pairGenerated == "QQ"||pairGenerated == "KK"||pairGenerated == "AA"){
            this.fullDeck.push(pairGenerated)
            } 

            //    PUSHING OFF-SUITED PAIRS TO THE GRID 
            else this.fullDeck.push(`${pairGenerated}`+"o")         
                
            }
              
          }          
      
        },

        selectHand(e){
        const _ = require('lodash');
        const hand = e.target.textContent.slice(0, -1)       

        !this.$store.state.raise.includes(hand) 
        ? this.$store.state.raise.push(hand) && (e.target.style.backgroundColor = `hsl(${this.$store.hue}, ${this.$store.saturation}%, ${this.$store.luminosity}%)`)
        : _.remove(this.$store.state.raise, (n) => n == `${hand}` ) && (e.target.style.backgroundColor = "rgb(204, 202, 202)");               
    },
                  
    }
}
</script>

<style>

.grid{
  font-size: 1rem;
  font-weight: bold;
}

.btn-choice{
  width: 5rem;
}


.title-choice-container{
  background-color: rgb(255, 255, 255);
  display: flex;
  flex-direction: row;
  width:775px;
  border: 3px solid rgb(255, 255, 255);
}

.title-choice{
  color: rgb(0, 0, 0);
  font-weight: bold;
  margin-right: 1rem;
}

.input-container{
  color:white;
  margin-top: 1.5rem ;
  margin-right: 10rem ;
  border: 1px solid rgb(255, 255, 255);
  padding: 1.5rem;
  border-radius: 3%;
}

.list{
  display:flex;
  flex-direction: column;
  align-items: flex-start;  
  height: 185px;
  width: 320px;
  border: 1px solid red;
  position: absolute ;
  bottom: 11.5%;
  right: 3%;
  background-color: white;
}

button{
  cursor: pointer;
  background-color: rgb(204, 202, 202);
}

.container{
  display: flex;
}

.box{
  width: fit-content;
  display: grid;
  grid-template-columns: repeat(13, 60px);
  grid-template-rows: repeat(13, 60px);
  text-align: center;
  align-self: center;
}

.box a{
  color: black;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
  cursor:pointer;
  border: 1px solid black;
}

.box a:hover{
  background-color: #27292A;
  color: rgb(255, 255, 255);
}

</style>