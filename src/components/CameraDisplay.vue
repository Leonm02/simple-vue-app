<template>

    <div class='ui container'>

        <div class="obereBox">
                
        <video v-if="!imageData.image" ref="video" class="camera-stream2" />
        <img v-else :src="imageData.image" v-bind:style="{transform: 'rotate(' + imageData.image_orientation + 'deg'}" class="camera-stream">
        <div class='ui divider'></div>

        </div>

        <div class="untereBox">
            <div class="icon-group">   
            <button  class="camera-icon" @click="captureImage">
                <i class="big camera icon" ></i>
                <p>Take Picture</p>
            </button>

            <button class="camera-icon" @click="cancelImage">
                <i class="big cancel icon"></i>
                <p>delete all</p>
            </button>
        </div>
        </div>
        

        <div class="GalleryBox">
            <img v-for="(imageData, index) in List" :key="index" :src="imageData.image" class="camera-stream" />
        </div>
        
    
    </div>



</template>

<script>


export default {
    

    data() {
        return {
            defaultImage: '../../src/assets/image.png',
            mediaStream: null,
            List:[],
            imageData: {
                image: '',
            },
        }
    },
    methods: {
        captureImage() {
            const mediaStreamTrack = this.mediaStream.getVideoTracks()[0]
            const imageCapture = new window.ImageCapture(mediaStreamTrack)
            let reader = new FileReader();
            return imageCapture.takePhoto().then(blob => {
                reader.readAsDataURL(blob)
                reader.onload = () => {
                    this.List.push({
                        image: reader.result,
                    }) 
                    console.log("Listenlänge: " + this.List.length);
                }
            })  
        },
        cancelImage() {
            this.imageData.image = null;
            this.showCameraModal = true;
            navigator.mediaDevices.getUserMedia({video: true})
            .then(mediaStream => {
                    this.$refs.video.srcObject = mediaStream;
                    this.$refs.video.play()
                    this.mediaStream = mediaStream                   
            }) 
        },

    },
    mounted() {
        navigator.mediaDevices.getUserMedia({video: true})
            .then(mediaStream => {
                    this.$refs.video.srcObject = mediaStream;
                    this.$refs.video.play()
                    this.mediaStream = mediaStream                   
            })   
    },
}
</script>

<style>
.GalleryBox{
    background-color: #3685fc;
    display: flex;
    flex-wrap: wrap;

}
.obereBox{
    background-color: #3e3e3e;
}
.untereBox{
    background-color: #c4c4c4;
    width: 500px;
    margin: auto;
}
.ui {
display: flex;
justify-content: center;
flex-direction: column;
background-color: #c4c4c4;
width: 100%;
height: auto;

}
    .icon-group {
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        margin: 12px auto;
    }
    
  .camera-icon {
  margin: auto;
  width: 35%;
  vertical-align: middle;
  padding: 15px 30px;
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  border-radius: 10px;
  border: 0px;
  font-weight: 700;
  box-shadow: 0px 0px 14px -7px #19acf0;
  background-image: linear-gradient(45deg, #2f6aff 0%, #19acf0  51%, #2f6aff  100%);
  cursor: pointer;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.camera-icon:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
}

.camera-icon:active {
  transform: scale(0.95);
}
    .camera-stream {
        margin: 10px 10px;
        width: 20%;
    }
    .camera-stream2 {
        margin: 10px 50px;
        width: 35%;
    }
     
</style>