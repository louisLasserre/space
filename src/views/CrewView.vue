<template>
    <div class="crewBack"></div>
    <section class="allContent crewContent" v-if="crewActiveOne">
        <div class="planet crewLeftP">

            <article class="pageTitle"><p>02</p><p>MEET YOUR CREW</p></article>

            <div class="crewInfos">
                <h2>{{ crewActiveOne.role }}</h2>
                <h1>{{crewActiveOne.name}}</h1>
                <p>{{crewActiveOne.bio}}</p>
            </div>
            
            <div class="btnContainer">
                <div class="btnCircle" v-for="member in crew" :class="member.name" :key="member.name" @click="active(member), styleActive()"></div>
            </div>
        </div> 
        <img :src="src" alt="">
    </section>
  
</template>

<script>
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
    active(id){
        
        
        this.crewActiveOne = id
        var url = id.images.png
        this.src = require("@/assets/crew/"+url)

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
    .crewBack{
        position: absolute;left: 0;right: 0;bottom: 0;top: 0;
    
        z-index: 0;
        background-image: url('../assets/crew/background-crew-desktop.jpg');
        background-repeat: no-repeat;
        background-size: cover;
    }
    .crewContent{
        position: fixed;bottom: 0;left: 0;right: 0;
        img{
            height: 70vh;
        }
    
        
    }
    .crewLeftP{
        width: 35vw;
        
        height: 70vh;
        justify-content: space-between;
        
        
    }
    

    .crewInfos{
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        
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
    }
    .btnCircle{
        background: rgba(255, 255, 255, 0.171);
        width: 15px;
        height: 15px;
        margin: 20px 15px;
        display: inline-block;
        z-index: 2;
        border-radius: 50%;


    }
    .planet article p{
        color: white;
    }
    @media only screen and (max-width: 770px) {
        .crewBack{
            background-image: url('../assets/crew/background-crew-tablet.jpg');
        }

    }
    @media only screen and (max-width: 500px) {
        .crewBack{
            background-image: url('../assets/crew/background-crew-mobile.jpg');
        }

    }

</style>