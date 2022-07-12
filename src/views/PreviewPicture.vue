<template>
    <div class="card">
        <div class="card-body">
            <h4 class="card-title">アップロードする画像を選択してください</h4>
            <input type="file" ref="file" accept="image/*" @change="onFileChange($event)">
            <img :src="imageData" v-if="imageData">
            <button class="btn btn-danger" v-if="imageData" @click="resetFile">リセットする</button>
        </div>
    </div>
</template>

<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: "PreviewPicture",
  props: {
  },
  data() {
    imageData: ''
  },
  methods: {  
    onFileChange(e) {

        const files = e.target.files;

        if(files.length > 0) {

            const file = files[0];
            const reader = new FileReader();
            reader.onload = (e) => {

                this.imageData = e.target.result;

            };
            reader.readAsDataURL(file);

        }

    },
    resetFile() {

        const input = this.$refs.file;
        input.type = 'text';
        input.type = 'file';
        this.imageData = '';

    }
}
})
</script>
