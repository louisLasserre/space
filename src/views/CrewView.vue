<template>
    <div class="crewBack"></div>
    <section class="allContent crewContent" v-if="crewActiveOne" @mousemove="move">
        <article class="pageTitle"><p>02</p><p>MEET YOUR CREW</p></article>
        <div class="planet crewLeftP">


            <div class="crewInfos">
                <h2 class="crewDy">{{ crewActiveOne.role }}</h2>
                <h1 class="crewDy">{{crewActiveOne.name}}</h1>
                <p class="crewDy">{{crewActiveOne.bio}}</p>
                
            </div>
            
            <div class="btnContainer">
                <div class="btnCircle" v-for="member in crew" :class="member.name" :key="member.name" @click="active(member)"></div>
                <button class="previous btnC" @click="prev"> <p class="btnP">prev</p> </button>
                <button class="next btnC" @click="next"> <p class="btnP">next</p> </button>
            </div>
        </div>
        <div class="astro-img">
            <img :src="src" alt="astronaute image">
        </div>
        
    </section>
  
</template>

<script>
import { parseQuery } from 'vue-router'
export default {
    mounted(){
        
        const border = document.getElementsByClassName('border')
    
        var width =  document.body.clientWidth
        if(width <= 770 && width > 380 ){
            console.log("tablet")
            border.border.style.left = '54.3%'
            border.border.style.width = '40px'

        }else if(width <= 380){
            console.log("mobile")
            border.border.style.left = '54.3%'
            border.border.style.width = '40px'

        }else{
            console.log("pc")
            border.border.style.left = '49.5%'
            border.border.style.width = '60px'
        }


        fetch('https://spacedblouis.herokuapp.com/crew')
            .then(res => res.json())
            .then(data => {
                this.crew = data
                this.crewActiveOne = data[0]
                
            })
            .then(() => {
                var url = this.crewActiveOne.images.png
                
                this.src = require("@/assets/crew/"+url)
                this.styleActive()
            })
            .catch(err => console.log(err.message))
  },
  methods: {
    prev() {
        var actualId = parseInt(this.crewActiveOne.id)
        if(actualId > 0 && actualId <= 3){
            actualId -= 1
        }else if(actualId == 0){
            actualId = 3
        }
        
        this.crew.forEach(member => {
            if(parseInt(member.id) ==  actualId){

                
                this.active(member)
            }
        });
        
    },
    next(){
        var actualId = parseInt(this.crewActiveOne.id)
        if(actualId >= 0 && actualId < 3){
            actualId += 1
        }else if(actualId == 3){
            actualId = 0
        }
        
        this.crew.forEach(member => {
            if(parseInt(member.id) ==  actualId){

                
                this.active(member)
            }
        });

    },
    move(){
        const btn = document.getElementsByClassName("btnC")
        const btnP = document.getElementsByClassName("btnP")
        
        for(let item of btn){
            
            item.style.backgroundColor = "rgba(255, 255, 255, 0.17)"
            item.style.backgroundColor = "2px solid rgba(255, 255, 255, 0.17)"
        }
        for(let text of btnP){
            text.style.color = "rgba(255, 255, 255, 0.5)"
        }
    },
    
    active(id){
        const crewBox = document.getElementsByClassName("crewDy")
        
        
        
        
        for(let item of crewBox){
            item.style.opacity = "0"
        }


       
        
        
        setTimeout(() => {
            this.crewActiveOne = id
            var url = id.images.png
            this.src = require("@/assets/crew/"+url)
            for(let item of crewBox){
                item.style.opacity = "1"
            }
            this.styleActive()
        },400)
        

        


    },
    styleActive() {
        console.log("active")
        const circle = document.getElementsByClassName(this.crewActiveOne.name)
        circle[0].style.backgroundColor = "white"
        
        

        this.crew.forEach(member => {
            
            if(this.crewActiveOne.name != member.name){
                
                let pp = document.getElementsByClassName(member.name)
                pp[0].style.backgroundColor = "rgba(255, 255, 255, 0.17)"
                
            }

            
        });
    }

  },
  data() {
      return {
          crew: [],
          crewActiveOne: null,
          src: null
      }
  }

}
</script>

<style lang="scss">
    body{
        height: 100%; 
        overflow: hidden;
    }
    .pageTitle{
        grid-area: pageTitle;
    }
    .crewBack{
        position: absolute;left: 0;right: 0;bottom: 0;top: 0;
    
        z-index: 0;
        background-image: url('../assets/crew/background-crew-desktop.jpg');
        background-repeat: no-repeat;
        background-size: cover;
    }
    .crewContent{
        position: fixed;bottom: 0;left: 0;right: 0;
        display: grid;
        grid-template-columns: auto auto ;
        grid-template-rows: repeat(2, auto);
        grid-template-areas: "pageTitle img"
                            "infos img";
        
        img{
            height: 70vh;
            
            
        }
        .astro-img{
            height: 100%;
            grid-area: img;

        }
        
    
        
    }
    .crewLeftP{
        width: 35vw;
        
        
        justify-content: space-between;
        transition: all 0.5s;
        
    }
    .crewDy{
        transition: all 0.3s;
        width: fit-content;
    }
    

    .crewInfos{
        grid-area: infos;
        position: relative;
        
        h1{
            font-size: 56px;
            margin: 10px 0 40px 0;
            
        }
        p{
            text-align: left;
            font-size: 18px;
            
        }
        h2{
            font-size: 32px;
            font-family: 'Bellefair', serif;
            color: rgba(255, 255, 255, 0.5);
            font-weight: 400;
            margin: 0;

            
        }
        
        
    }
    .btnContainer{
        
        padding-bottom: 40px;
        position: relative;
        button{
            width: 50px;
            height: 50px;
            background-color: rgba(255, 255, 255, 0);
            border: 2px solid rgba(255, 255, 255, 0);
            border-radius: 50%;
            cursor: pointer;
            position: absolute;
            top: 0;
            transition: all 0.3s;
            
            text-align: center;
            p{
                color: rgba(0, 0, 0, 0);
                width: fit-content;
                margin: 0;
                position: absolute;
                top: 50%;left: 50%;
                transform: translate(-50%, -50%);

                
            }
        }
        .previous{
            left: 0;
            transform: translateX(-100%);
        }
        .next{
            right: 0;
            transform: translateX(100%);
        }
    }
    .btnCircle{
        background: rgba(255, 255, 255, 0.171);
        width: 15px;
        height: 15px;
        margin: 20px 15px;
        display: inline-block;
        z-index: 2;
        border-radius: 50%;
        transition: all 0.3s;
        cursor: pointer;
        &:hover{
            background: rgba(255, 255, 255, 0.5) !important;
        }


    }
    .planet article p{
        color: white;
    }
    @media only screen and (max-width: 770px) {
        .crewBack{
            background-image: url('../assets/crew/background-crew-tablet.jpg');
        }
        .planet{
            align-items: center;
            .crewDy{
                width: 100%;
            }
        }
        .crewContent{
            /*changement de la grid*/
           
            width: 90%;
            margin: 0 auto;
            height: 90%;
            grid-template-columns: 100%;
            grid-template-rows: 70px repeat(2, auto);
            grid-template-areas:"pageTitle"
                                "infos"
                                "img";
            
            .astro-img{
                position: relative;
                height: 100%;
                min-height: 250px;

            }
            img{
                height: 100%;
                min-height: 250px;
                
                position: absolute;bottom: 0;
                left: 50%;
                transform: translateX(-50%);


            }
        }
         
        .btnCircle{
            width: 10px;
            height: 10px;
        }
        .crewLeftP{
            height: auto;
            width: 100%;
            margin-top: 20px;
            .crewInfos{
                width: 60vw;margin: 0 auto;
                align-items: center;
                h2{
                    margin-top: 20px;
                }
                h1{
                    margin-top: 0;
                }
                p{
                    margin-bottom: 20px;
                }
            }
            .btnContainer{
                margin: 0 auto;
                button{
                    background-color: rgba(255, 255, 255, 0.178);
                    border: 2px solid rgba(255, 255, 255, 0);
                    p{
                        color: rgba(255, 255, 255, 0.507);
                    }
                }
            }
            .crewDy{
                text-align: center;
            }
        }

    }
    @media only screen and (max-width: 500px) {
        .crewBack{
            background-image: url('../assets/crew/background-crew-mobile.jpg');
        }
        .crewContent {
            .astro-img{
                min-height: 200px;
            }
            .astro-img::after{
                content: "";
                
                width: 90vw;
                position: absolute;bottom: -3px;left: 0;
                
                border-bottom: 3px solid rgba(255, 255, 255, 0.178);
                
            }
            img{
               min-height: 200px; 
               height: 100%;
               
            }
        }
        .crewContent{
            /*changement de la grid*/
            grid-template-areas:"pageTitle"
                                "img"
                                "infos";
            article{
                margin: 0 auto;
            }
        }
        .allContent .crewLeftP {
            margin-top: 0;
            align-items: center;
            justify-content: unset;
            display: grid;
            grid-template-columns: auto;
            grid-template-rows: auto auto;
            grid-template-areas:
                "boutons"
                "texte";
            .crewInfos{
                grid-area: texte;
                width: 100%;
                height: 100%;
                h2{margin-top: 6%;}
                h1{margin-bottom: 6%;}
                p{margin-bottom: 3%;}
            }
            .btnContainer{
                grid-area: boutons;
                padding-bottom: 0;
            }
            
        }

    }

</style>