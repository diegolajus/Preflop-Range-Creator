<template>
    <div>
        <div class="color-picker-container">
            <color-picker  v-bind="color" @input="onInput"></color-picker>
        </div>
    </div>
</template>

<script>
import ColorPicker from '@radial-color-picker/vue-color-picker';

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
}

.download-button-container{
    color:white;
    height:150px; 
}

@import '~@radial-color-picker/vue-color-picker/dist/vue-color-picker.min.css';

</style>
