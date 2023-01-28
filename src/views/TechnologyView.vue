<template>
  <section class="technoBack"></section>
  <div class="techno-grid">
        <article class="pageTitle"><p>03</p><p>SPACE LAUNCH 101</p></article>
        <div class="techno-btn-container">
            <nav class="techno-btn" v-for="tech in technology" :id="tech.id" :key="tech.id" @click="active(tech)"><h3>{{ tech.id+1 }}</h3></nav>

        </div>
        <article class="techno-texte">
            <article>
                <div class="inner-article" v-for="tech in technology" :id="tech.id+10" :key="tech.id+10">
                    <h4>THE TERMINOLOGY ...</h4>
                    <h1>{{ tech.name }}</h1>
                    <p>{{ tech.description }}</p>
                </div>
            </article>
        </article>
        <div class="techno-img">
            <img :src="src" alt="image de fusée">
        </div>
  </div>
</template>

<script>
export default {
    data() {
        return{
            technology: [],
            technoActive: [],
            src: null,


        }
    },
    mounted(){

        var width =  document.body.clientWidth

        fetch('https://space-db.osc-fr1.scalingo.io/technology')
            .then(res => res.json())
            .then(data => {
                this.technology = data
                this.technoActive = data[0]

            })
            .then(() => {
                var url = this.technoActive.images.portrait
                var smallUrl = this.technoActive.images.landscape
                if(width <= 770){
                    this.src = require("@/assets/technology/"+smallUrl)
                }else{

                    this.src = require("@/assets/technology/"+url)
                }
                this.styleActive()
            })
            .catch(err => console.log(err.message))


        const border = document.getElementsByClassName('border')


        if(width <= 770 && width > 500 ){
            console.log("tablet")
            border.border.style.left = '70%'
            border.border.style.width = '80px'



        }else if(width <= 500){
            console.log("mobile")
            border.border.style.left = '70%'
            border.border.style.width = '80px'

        }else{
            console.log("pc")
            border.border.style.left = '65.3%'
            border.border.style.width = '90px'
        }
    },
    methods: {
        active(id){
            //const technoBtn = document.getElementsByClassName("techno-btn")

            const width = document.body.clientWidth
            this.technoActive = id

            var url = id.images.portrait
            var smallurl = id.images.landscape

            if (width <= 770) {
                var anim = "translateX"

            }else{
                var anim = "translateY"
            }

            const technoTxt = document.getElementsByClassName("techno-texte")

            if(id.id == 0){
                technoTxt[0].firstChild.style.transform = anim+"(0%)"
            }else if(id.id == 1){
                technoTxt[0].firstChild.style.transform = anim+"(-100%)"
            }else if(id.id == 2){
                technoTxt[0].firstChild.style.transform = anim+"(-200%)"
            }


            const img = document.getElementsByClassName("techno-img")

            img[0].firstChild.style.opacity = "0"





            setTimeout(() => {
                if(width <= 770){
                    this.src = require("@/assets/technology/"+ smallurl)
                }else{

                    this.src = require("@/assets/technology/"+ url)
                }
                img[0].firstChild.style.opacity = "1"

            },250)
            this.styleActive()




        },
        styleActive() {

            const circle = document.getElementById(this.technoActive.id)

            circle.style.backgroundColor = "white"
            circle.firstChild.style.color = "black"



            this.technology.forEach(tech => {

                if(this.technoActive.id != tech.id){

                    let pp = document.getElementById(tech.id)
                    pp.style.backgroundColor = "transparent"
                    pp.firstChild.style.color = "white"

                }


            });
        }
    }


}
</script>

<style lang="scss">


    .technoBack{
        position: absolute;
        left: 0;right: 0;bottom: 0;top: 0;

        z-index: 0;
        background-image: url('../assets/technology/background-technology-desktop.jpg');
        background-repeat: no-repeat;
        background-size: cover;
    }
    .techno-grid{
        position: fixed;bottom: 0;left: 12vw;right: 0;
        height: 70vh;padding: 10vh 0;
        z-index: 1;

        display: grid;
        grid-template-columns: repeat(3, auto);
        grid-template-rows: 9vh 61vh;
        grid-template-areas:"pageTitle pageTitle pageTitle"
                            "btnBox texte img";

        & .pageTitle{


        }
        & > .techno-btn-container{
            grid-area: btnBox;
            padding: 90px 0;
            min-height: 240px;
            display: flex;flex-direction: column;
            justify-content: space-evenly;
            align-items: flex-start;
            width: fit-content;
        }
        & > .techno-texte{

            margin: 90px 0;
            min-height: 240px;

            grid-area: texte;
            overflow: hidden;

            .inner-article{
                height: 100%;
                width: 80%;
                margin: 0 auto;

            }
            & > article{
                height: 100%;
                width: 100%;
                transition: all 0.5s;
            }
        }
        & .techno-img{
            grid-area: img;
            min-height: 408px;
            height: 100%;
            img{
                height: 100%;
                transition: all 0.25s;
            }

        }
    }
    .techno-btn-container nav {
        width: 80px;height: 80px;
        display: grid;
        place-items: center;
        background: transparent;
        border: 1px solid rgba(255, 255, 255, 0.253);
        border-radius: 50%;

        cursor: pointer;
        transition: all 0.4s ;


        h3{
            font-family: 'Bellfair', serif !important;
            font-weight: normal;
            font-size: 32px;
            width: fit-content;
            display: inline;
        }

    }
    .techno-btn-container nav:hover {
        border: 1px solid white;
    }
    .inner-article{
        text-align: left;
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;

        h4{
            font-size: 16px;
            color: #D0D6F9;
            margin: 0;
        }
        h1{
            font-size: 56px;
        }
        p{
            font-size: 18px;
            color :#D0D6F9;
            line-height: 35px;
        }

    }



    @media only screen and (max-width: 770px) {
        $imageHeight: calc(768px / 310px);
        .technoBack{
            background-image: url('../assets/technology/background-technology-tablet.jpg');
            background-position: center;
        }
        .techno-grid{
            grid-template-columns: 100vw;
            grid-template-rows: minmax(60px, 85px) calc(100vw / $imageHeight)  minmax(120px, 190px) auto;
            grid-template-areas:"pageTitle"
                                "img"
                                "btnBox"
                                "texte";
            left: 0;
            padding: 0 0 50px 0;
            height: 83vh;
            .techno-img{

                height: fit-content;
                min-height: unset;
                position: relative;
                width: 100vw;
                img{


                    width: 100%;
                    height: unset;
                }

            }
            .techno-texte{
                padding: 0;
                min-height: 190px;
                article{
                    display: flex;

                }
                .inner-article{
                    text-align: center;
                    min-width: 80vw;
                    margin: 0 10vw;
                }
                h4{

                }
                h1{
                    font-size: 40px;
                }
                p{
                    font-size: 16px;
                }
            }
            .techno-btn-container{
                flex-direction: row;
                align-items: center;
                justify-content: space-evenly;
                height: 100%;
                min-height: 100%;
                width: 70%;
                margin: 0 auto;
                padding: 0;


            }
            .pageTitle{
                height: 100%;
                margin-left: 50px;

            }

        }

    }

    @media only screen and (max-width: 500px) {
        $imageHeight: calc(768px / 310px);
        .technoBack{
            background-image: url('../assets/technology/background-technology-mobile.jpg');
        }
        .techno-grid{

            grid-template-rows: minmax(46px, 57px) calc(100vw / $imageHeight)  minmax(70px, 114px) auto;

            .pageTitle{
                p{
                    font-size: 16px;

                }
                margin: 0 auto;
            }
            .techno-btn-container nav {
                width: 50px;
                height: 50px;
                h3{
                    font-size: 16px;
                }

            }
        }
    }

</style>
