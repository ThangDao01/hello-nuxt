<template>
  <div>
    <input type='file' @change='onFileSelected'>
    <button @click='onUpload'>Upload</button>
  </div>
</template>

<script>
export default {
  layout: null,
  data() {
    return {
      selectedFile: null
    }
  },
  methods: {
    onFileSelected(event) {
      this.selectedFile = event.target.files[0]
    },
    onUpload() {
      const file = new FormData();
      file.append('file',this.selectedFile,this.selectedFile.name)
      const uri = 'http://localhost:8000/api/import-csv';
      this.$axios.post(uri,file).then(res =>{
        console.log(res)
      })
    }
  }
}
</script>
