<template>
    <div>
        <div class="color-picker-container">
            <h3>1. Pick a color </h3>
            <color-picker  v-bind="color" @input="onInput"></color-picker>
        </div>
        
        <div class="download-button-container">
            <h3>3. Download Table </h3>
            <button class="download-button"  @click="makePDF"> GENERATE .JPG</button>
            <p>{{ filename }}</p>
        </div>
    </div>
</template>

<script>
import ColorPicker from '@radial-color-picker/vue-color-picker';
import domtoimage from 'dom-to-image';

export default {
    components: { ColorPicker },
    data() {
        return {
            color: {
                hue: 50,
                saturation: 100,
                luminosity: 50,
                alpha: 1
            },
            filename:"",
 
        };
    },
    
    methods: {
        makePDF(){
domtoimage.toJpeg(document.getElementById('my-node'), { quality: 0.95 })
    .then(function (dataUrl) {
        var link = document.createElement('a');
        link.download = 'my-image-name.jpeg';
        link.href = dataUrl;
        link.click();
    });
        },
        onInput(hue) {
            this.color.hue = hue;
            this.$store.hue = this.color.hue.toFixed()
            this.$store.saturation= this.color.saturation.toFixed()
            this.$store.luminosity= this.color.luminosity.toFixed()
            this.$store.alpha= this.color.alpha.toFixed()

        },
     
        },
           

};
</script>

<style>
.download-button{
    height: 3rem;
    border-radius: 5%;
}

.color-picker-container{
    color:white;
    border: 1px solid rgb(255, 255, 255);
    border-radius:15px;
    height:400px;
    padding: 1.5rem;
    margin: 1.5rem;
}

.download-button-container{
    color:white;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    border: 1px solid rgb(255, 255, 255);
    border-radius:15px;
    height:150px; 
    padding:2rem;
}

@import '~@radial-color-picker/vue-color-picker/dist/vue-color-picker.min.css';

</style>
