<template>
<div id="app">
    <nav class="navbar navbar-expand-md navbar-dark bg-dark fixed-top justify-content-center">
        <a class="navbar-brand">{{ msg }}</a>
    </nav>
    <img id="logo" src="./assets/logo.png" width="100px" height="100px">
    <table align="center">
    <nav aria-label="...">
  <ul class="pagination">
    <li class="page-item" :class="{disabled: pagePreviuosDisable}">
      <a class="page-link" @click="showPage(currentPage-1)">Previous</a>
    </li>
    <li v-for="(page,index) in listPage" :key="index" class="page-item">
        <a v-if="checkActive(page)" class="page-link isCurrent" @click="showPage(page)">{{ page }}</a>
        <a v-else class="page-link" @click="showPage(page)">{{ page }}</a>
        </li>
    <li class="page-item" :class="{disabled: pageNextDisable}">
      <a class="page-link" @click="showPage(currentPage+1)">Next</a>
    </li>
  </ul>
</nav>
    </table>
    <vue-picture-swipe :items="images"></vue-picture-swipe>

</div>
</template>

<script>
import VuePictureSwipe from 'vue-picture-swipe';
export default {
    name: 'app',
    components: {
        VuePictureSwipe
    },
    data() {
        return {
            msg: '10,000 images from https://thispersondoesnotexist.com/',
            images: [],
            listPage: [1,2,3,4,5,6,7,8,9,10],
            currentPage: 1,
            pagePreviuosDisable: true,
            pageNextDisable: false
        }
    },
    created() {
        for (var i = 1; i <= 1000; i++) {
            this.images.push({
                src: '../faces/dir1/image' + i + '.jpg',
                thumbnail: '../faces/dir1_thumbnail/image' + i + '.jpg',
                w: 900,
                h: 900
            })
        }
    },
    methods: {
        showPage(page){
            var startIndex=(page-1)*1000+1;
            this.images=[];
            this.currentPage=page;
            if(page==this.listPage[this.listPage.length-1]) this.pageNextDisable=true;
            else this.pageNextDisable=false;
            if(page==1) this.pagePreviuosDisable=true;
            else this.pagePreviuosDisable=false;
            for (var i = startIndex; i <= startIndex+999; i++) {
            this.images.push({
                src: '../faces/dir'+page+'/image' + i + '.jpg',
                thumbnail: '../faces/dir'+page+'_thumbnail/image' + i + '.jpg',
                w: 900,
                h: 900
            })
        }
        },
        checkActive(page){
            return page==this.currentPage;
        }
    }
}
</script>

<style>
@import 'https://code.jquery.com/jquery-3.4.1.slim.min.js';
@import 'https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js';
@import 'https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css';
@import 'https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js';
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

h1,
h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}

.isCurrent{
    color: white;
    background-color: #007BFF;
}

.pswp__img{
    border-radius: 5px;
}
img:hover:not(#logo):not(.pswp__img){
  -ms-transform: scale(1.5); /* IE 9 */
  -webkit-transform: scale(1.5); /* Safari 3-8 */
  transform: scale(1.5); 
  transition: .3s ease;
}
</style>
