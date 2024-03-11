<template>
  <body>
  <div id="editor"></div>
</body>
</template>

<script>
import Editor from '@toast-ui/editor';
import '@toast-ui/editor/dist/toastui-editor.css'; // Editor's Style

export default {
  data(){
    return {
      editer: null
    }
  },
  mounted(){
    this.editer =  new Editor({
      el: document.querySelector('#editor'),
      height: '500px',
      initialEditType: 'markdown',
      previewStyle: 'vertical',
      hooks:{
        addImageBlobHook: async (blob, calback) =>{
          // 1. 다른서버에 이미지 업로드 위임
          const uploadResult =await this.uploadImage(blob);
          // 2. 1에서 업로드 된 이미지를 접근할 수 있게 url 세팅
          calback(uploadResult.imageAccessUri);
        }
      }
    });
  },
  methods: {
    async uloadImage (blob){
      const formData = new FormData();
      formData.append('image',blob);

      const option = {
        method:'POST',
        body: formData
      }
      let response =await fetch('http://localhost:8080/upload', options);
      let result = response.json();

      return result;
    }
  }
}
</script>
