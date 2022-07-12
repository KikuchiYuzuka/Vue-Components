<template>
    <div class="container">
        <div class="row" v-if="!uploading">
            <div class="col-6">
                <input type="file" @change="onSelectFile">
            </div>
            <div class="col-6">
                <button type="button" class="btn btn-outline-primary" @click="onSubmit">送信</button>
            </div>
        </div>
        <div class="row" v-else>
            <div class="col-12 text-center">
                <progress ref="progress" value="0" max="100"></progress>
                <br>
                <span class="text-muted">アップロード中...</span>
            </div>
        </div>
    </div>
</template>

<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: "ProgreeBar",
  props: {
  },
  data() {
    file: null,
    uploading: false
  },
  methods: { 
    onSubmit() {
        const url = '/progress';
        let formData = new FormData();
        formData.append('file', this.file);
        if(this.file === null) {
            alert('ファイルを選択してください');
            return;
        }

        this.uploading = true;

        axios.post(url, formData, { onUploadProgress: this.onUpload })
            .then((response) => {
                alert('アップロードが完了しました！');
            })
            .catch((error) => {

            })
            .then(() => {
                this.$refs.progress.value = 0; 
                this.uploading = false;
            });
    },
    onSelectFile(e) {   
        const files = e.target.files;
        if(files.length === 0) {  
            this.file = null;
            return;
        }
        this.file = files[0];
    },
    onUpload(e) {
        this.$refs.progress.value = Math.floor((e.loaded * 100) / e.total);
    } 
  }
</script>


