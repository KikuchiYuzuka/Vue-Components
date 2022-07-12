<template>
    <h1>選択機能をつけた画像ギャラリー</h1>
        <div :class="imageCss(index)" v-for="(imageUrl,index) in imageUrls">
            <i class="fa fa-check-circle icon" v-if="isSelected(index)"></i>
            <img :src="imageUrl" @click="onImageSelect(index)">
        </div>
        <div style="width:100%;position:fixed;bottom:0;left:0;background:#ddd;" v-if="selectedIndexes.length">
            <div style="padding:15px;">
                <button @click="clear"><i class="fa fa-times"></i> 選択解除</button>
                <span style="padding-left:30px;" v-text="selectedIndexes.length"></span> 件
                <button style="margin-left:30px;" @click="close"><i class="fa fa-trash-alt"></i> 削除</button>
            </div>
        </div>
</template>

<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: "SelectImages",
  props: {

  },
    data() {
    imageUrls: [
        './images/yummy/1.jpg',
        './images/yummy/2.jpg',
        './images/yummy/3.jpg',
        './images/yummy/4.jpg',
        './images/yummy/5.jpg'
    ],
    selectedIndexes: []  
    },
    methods: {
        isSelected(index) {
            return (this.selectedIndexes.includes(index));
        },
        imageCss(imageIndex) {
            let classes = ['selectable-box'];
            if(this.isSelected(imageIndex)) { 
                classes.push('active');
            }
            return classes;
        },
        clear() {
            this.selectedIndexes = [];
        },
        close() {
            let newImageUrls = [];

            for(let i = 0 ; i < this.imageUrls.length ; i++) {
                if(!this.isSelected(i)) {
                    newImageUrls.push(this.imageUrls[i]);
                }
            }
            this.imageUrls = newImageUrls;
            this.selectedIndexes = [];
            alert('削除が完了しました。');
        },
        onImageSelect(imageIndex) {
            if(this.isSelected(imageIndex)) {
                this.selectedIndexes = this.selectedIndexes.filter((selectedIndex) => {
                    return (selectedIndex !== imageIndex);
                });
            } else {
                this.selectedIndexes.push(imageIndex);
            }
        }
    }
})
</script>
