<template>
  <div>
    <v-row>
      <v-col v-if="!showCard" cols="12">
        <v-btn color="primary" icon @click="setFlag()"><v-icon>mdi-arrow-left</v-icon> </v-btn>
      </v-col>
      <v-col :cols=" showCard ? 12 : 6 ">
        <v-card flat height="400" v-if="showCard" class="text-center ma-5" style="border:2px dashed #64B5F6 ">
          <v-row style="height:100%" align="center">
            <v-col cols="12">
              <div class="text-h6 font-weight-bold">  <v-icon>mdi-image</v-icon> Upload Image</div>
              <div><small> Supported formats are PNG SVG JPEG, GIF *</small></div>
              <small><b>Note: upload a High quality image to see accurate results. </b></small>
              <div class="mt-3">
                <v-btn icon @click="selectFile()">
                  <v-icon color="#64B5F6" size="85">mdi-cloud-upload</v-icon>
                </v-btn>
                <v-file-input name="image" style="display:none" @change="uploadFile()" label="File input" v-model="selectImage" accept="image/*" ref="fileInput"></v-file-input>
              </div>
            </v-col>
          </v-row>
        </v-card>
        <v-card flat class="text-center">
          <v-col cols="12">
            <div>
              <img :src="imageSrc" width="500" height="500" v-if="imageSrc" alt="Selected Image">
            </div>
          </v-col>
        </v-card>
      </v-col>
      <v-col cols="6" v-if="!showCard">
        <span class="font-weight-bold">See extracted text here...</span>
          <v-col cols="12">
            <v-progress-linear indeterminate v-if="loading" color="#64B5F6"></v-progress-linear>
             <div>{{text}}</div>
          </v-col>
      </v-col>
    </v-row>
  </div>
</template>
<script>
import { api } from '../plugins/axios_settings'
export default {
data() {
  return {
      selectImage: null,
      loading: false,
      text: '',
      imageSrc: '',
      showCard: true
  }
},
methods: {
    selectFile() {
      this.$refs.fileInput.$refs.input.click()
    },
    uploadFile() {
      this.loading = true
      var filesList = this.selectImage
      var formData = new FormData()
      formData.append('image', filesList)
        const reader = new FileReader()

      reader.onload = (event) => {
        this.imageSrc = event.target.result
        this.showCard = false
      }

      reader.readAsDataURL(filesList)
       api.post('image/upload-image',formData,{
        headers: {
             'Content-Type': 'multipart/form-data'
              }
        }
       ).then((response) => {
            this.loading = false
            this.text = response.data.data.imageText
    })
    },
    setFlag () {
        this.showCard = true
        this.imageSrc = ''
        this.text = ''
    }
}
}
</script>