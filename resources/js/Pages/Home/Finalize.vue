<template>
    <div>
        <div v-if="content" class="content" id="capture">
            <div class="header">
                <h1 class="title">Tastetify</h1>
                <span>{{ time_frame }} Best Menu by {{ user.name }}</span>
            </div>
            <hr class="text-white">
            <ul>
                <li v-for="(track, index) in tracks" :key="index">
                    <div class="d-flex justify-content-between">
                        <div class="track text-white">
                            {{ track.title }} <span class="artist">by {{ track.artists }}</span>
                        </div>
                        <div class="px-3 pr-0 duration text-white">
                            {{ track.duration }}
                        </div>
                    </div>
                </li>
            </ul>

            <div class="d-flex images justify-content-between mt-4">
                
                <div v-for="(image, index) in images" :key="index" v-bind:style="{ backgroundImage: 'url(' + image + ')' }"></div>
                
            </div>

            <div>
                <p class="footer">Thanks for visiting us!</p>
            </div>
        </div>

        <div id="canvasRendered"></div>
    </div>
</template>

<script>

export default {
    props: {
        user: Object,
        tracks: Array,
        images: Array,
        time_frame: String
    },
    data() {
        return {
            output: null,
            content: true,
        }
    },
    methods: {
        screenshot(){
            const html2canvas = require('html2canvas');
            html2canvas(document.getElementById('capture'), {
                allowTaint: true
            }).then(function(canvas){
                document.getElementById('canvasRendered').append(canvas)
                
            });
            this.content = false
        }
    },
    mounted() {
        //this.print()
        this.screenshot()
    }
}
</script>

<style scoped>
.header {
    margin-bottom: 0;
}

h1.title {
    font-size: 34px;
    margin-bottom: 0;
    color: #ffe100;
}

.header span {
    font-size: 12px;
    margin-left: 8px;
    color: #ffe100;
}

ul {
    margin: 0;
    padding: 0;
    list-style: none;
}
li {
    margin-bottom: 8px;
}
.content {
    max-width: 380px;
    padding: 1.3rem;
    background-image: url('/img/texture2.jpg');
    background-position: center center;
    background-size: cover;
    background-color: rgb(0, 0, 0);
    border:0;
}
.pr-0 {
    padding-right: 0!important;
}

.track {
    font-size: 15px;
}

.duration {
    font-size: 13.5px;
}

span.artist {
    display: block;
    font-size: 11.5px;
}

.images div {
    width: 100px;
    height: 100px;
    background-size: cover;
    border: 1px solid grey;
    border-radius: 8px;
}

p.footer {
    color: #ffe100;
    text-align: center;
    margin-top: 18px;
    margin-bottom: 0;
    font-size: 12px;
}

#canvasRendered {
    margin: 20px auto;
    text-align: center;
}

</style>