<template>
        <div class="container">

            <div><ColorPicker/></div>
            <div>
              <div class="input-container">
                <div class="input-group">
                  <input class="input" v-model="message1" type="text">
                  <a class="delete-btn" v-on:click="deleteInput1" >&#10006;</a>
                </div>
                <div class="input-group">
                  <input class="input" v-model="message2" type="text">
                  <a class="delete-btn" v-on:click="deleteInput2" >&#10006;</a>
                </div>
                <div class="input-group">
                  <input class="input" v-model="message3" type="text">
                  <a class="delete-btn" v-on:click="deleteInput3" >&#10006;</a>
                </div>
                <div class="input-group">
                  <input class="input" v-model="message4" type="text">
                  <a class="delete-btn" v-on:click="deleteInput4" >&#10006;</a>
                </div>
                <div class="input-group">
                  <input class="input" v-model="message5" type="text">
                  <a class="delete-btn" v-on:click="deleteInput5" >&#10006;</a>
                </div>
              </div>
            </div>



          <div class="box" id="my-node">
            <button   class="grow grid" v-on:click="selectHand" v-for="item in this.fullDeck" :key="item">{{item}} </button>
            <div class="title-choice-container">              
              <button ref="msg1" v-on:click="selectHand" class="btn-choice title-choice">{{ message1 }}</button>
              <button ref="msg2" v-on:click="selectHand" class="btn-choice title-choice">{{ message2 }}</button>
              <button ref="msg3" v-on:click="selectHand" class="btn-choice title-choice">{{ message3 }}</button>
              <button ref="msg4" v-on:click="selectHand" class="btn-choice title-choice">{{ message4 }}</button>
              <button ref="msg5" v-on:click="selectHand" class="btn-choice title-choice">{{ message5 }}</button>

            </div>
          </div>

          
        <div class="download-button-container">
            <button class="download-button"  @click="makePDF"> GENERATE .JPG</button>
            <p>{{ filename }}</p>
        </div>

        <div>
          <How/>
        </div>
        </div>
</template>



<script>
import ColorPicker from '../components/ColorPicker.vue'
import How from '../components/How.vue'
import domtoimage from 'dom-to-image';

export default {
  components: {
    ColorPicker,How
  },
data() {
        
        const firstCard = ["A", "K", "Q","J","T","9","8","7","6","5","4","3","2"]
        const secondCard = ["A","K","Q","J","T","9","8","7","6","5","4","3","2"]
        const fullDeck = []

        return {
            firstCard,
            secondCard,
            fullDeck,
            message1:"Open Raise",   
            message2:"Call 4Bet",   
            message3:"Fold vs Tight",
            message4:"Raise Over Limpers",
            message5:"Fold vs Loose",
            filename:"",
            color: {
                hue: 50,
                saturation: 100,
                luminosity: 50,
                alpha: 1
            },
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
        : _.remove(this.$store.state.raise, (n) => n == `${hand}` ) && (e.target.style.backgroundColor = "rgb(160, 160, 160)");               
    },
        deleteInput1(e){
          e.target.parentElement.remove()
          this.$refs.msg1.remove()
    },
        deleteInput2(e){
          e.target.parentElement.remove()
          this.$refs.msg2.remove()
    },
            deleteInput3(e){
          e.target.parentElement.remove()
          this.$refs.msg3.remove()
    },
            deleteInput4(e){
          e.target.parentElement.remove()
          this.$refs.msg4.remove()
    },
            deleteInput5(e){
          e.target.parentElement.remove()
          this.$refs.msg5.remove()
    },
            makePDF(){
domtoimage.toJpeg(document.getElementById('my-node'), { quality: 0.95 })
    .then(function (dataUrl) {
        var link = document.createElement('a');
        link.download = 'my-image-name.jpeg';
        link.href = dataUrl;
        link.click();
    });
        },
    }
}
</script>

<style>

.grid{
  font-size: 1rem;
  font-weight: bold;
  background-color: rgb(160, 160, 160);
  border-radius: 5%;
}

.btn-choice{
  width: 5rem;
  background-color: rgb(160, 160, 160);

}


.title-choice-container{
  background-color: rgb(221, 221, 221);
  display: flex;
  justify-content: center;
  flex-direction: row;
  width:775px;
  border: 2px solid rgb(255, 255, 255);
  height: 50px;
}

.title-choice{
  color: rgb(0, 0, 0);
  font-weight: bold;
  margin-right: 1rem;
  width: fit fit-content;
}

.input-container{
  width: 300px;
  color:white;
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
}

.container{
  display: flex;
  flex-direction: row;
  align-items: center;
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

.delete-btn{
  font-size: 1.5rem;
  cursor: pointer;
  margin-left: 10px;
}

.input-group{
  display: flex;
  justify-content: center;
  margin: 80px;

}
.input{
  text-align: center;
  height: 25px;
  width: 125px;
  
}

.download-button-container{
  display: flex;
    color:white;
    margin: 100px;

}

.download-button{
    height: 3rem;
    border-radius: 5%;
}
</style>