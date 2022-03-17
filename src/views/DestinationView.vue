<template>
  Destination view
    <section class="Dest"></section>

    <section class="allContent" v-if="activeOne">
        <div class="planet" style="">
            <article><p>01</p><p>PICK YOUR DESTINATION</p></article>
            <img :src="src" alt="">
            <!--<img src="../assets/destination/image-moon.png" alt="">-->
        </div>
        <div class="infos">
            <div class="infosbar">

                <div class="planetName" v-for="dest in destination" :key="dest.name"> 
                    <p @click="active(dest)">{{ dest.name }}</p>
                </div>
            </div>
            <h1 @click="click(activeOne.images.png)">{{ activeOne.name }}</h1>
            <p>{{ activeOne.description }}</p>
            <div class="infotrait"></div>
            <section class="infoNbr">
                <div>
                    <p>AVG. DISTANCE</p>
                    <h3>{{ activeOne.distance}}</h3>
                </div>
                <div>
                    <p>EST. TRAVEL TIME</p>
                    <h3>{{ activeOne.travel}}</h3>
                    
                </div>
            </section>
        </div>
        
        
        
        
    </section>

    
</template>

<script>
export default {
    data() {
        return{
            destination: [],
            activeOne: null,
            src: null,
            test: null
        }
    },
    methods: {
        active(id){
            
            console.log(id)
            this.activeOne = id
            var url = id.images.png
            this.src = require("@/assets/destination/"+url)


        },
        imgUrl(){
            
        },
        click(url) {
            
            
            this.test = true
        }
    },
    beforeMount(){
    
        const border = document.getElementsByClassName('border')
    
        var width =  document.body.clientWidth
        if(width <= 770 && width > 500 ){
            console.log("tablet")
            border.border.style.left = '29.5%'
            border.border.style.width = '80px'

        }else if(width <= 500){
            console.log("mobile")
            border.border.style.left = '29.5%'
            border.border.style.width = '80px'

        }else{
            console.log("pc")
            border.border.style.left = '30%'
            border.border.style.width = '90px'
        }

        fetch('http://localhost:3000/destinations')
            .then(res => res.json())
            .then(data => {
                this.destination = data
                this.activeOne = data[0]
                
            })
            .then(() => {
                var url = this.activeOne.images.png
                this.src = require("@/assets/destination/"+url)
            })
            .catch(err => console.log(err.message))

            
        

        
    },
    mounted() {
        

    }
    

}
</script>

<style lang="scss">
    .Dest{
        position: absolute;left: 0;right: 0;bottom: 0;top: 0;
    
        z-index: 0;
        background-image: url('../assets/destination/background-destination-desktop.jpg');
        background-repeat: no-repeat;
        background-size: cover;
    }
    .allContent{
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        position: relative;
        z-index: 1;
        margin-top: 40px;
        padding: 0 10vw;
        p{
            color: #D0D6F9;
        }
        .planet{
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            img{
                margin-left: 65px;
                margin-top: 50px;
                width: 445px;
            }
            article{
                p{
                    display: inline;
                    font-size: 28px;
                }
                p:first-child{
                    margin-right: 20px ;
                    font-weight: 800;
                    color: rgba(255, 255, 255, 0.26);
                }
            }

        }
        .infos{
            width: 30vw;
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            margin-top: 30px;
            .infosbar{
                display: flex;
                margin-bottom: 30px;
                .planetName:first-child{
                    margin-left: 0;
                }
                
            }
            .planetName{
                margin: 0 20px;
            }
            p{
                font-size: 18px;
                text-align: left;
                margin-top: 20px;
                line-height: 32px;
                

            }
            h1{
                font-size: 100px;
            }
            .infotrait{
                width: 100%;
                height: 1px;
                background: #383B4B;
                margin: 40px 0 20px 0;
            }
            .infoNbr{
                display: flex;
                h3{
                    width: fit-content;
                    font-family: 'Bellefair', serif !important;
                    font-size: 38px;
                }
                & :first-child{
                    margin-right: 60px;
                }

            }
        }
    }
    //tablet
    @media only screen and (max-width: 770px) {
        .allContent{
            flex-direction: column;
            padding: 0 39px;
            align-items: center;
            .planet{
                width: 100%;
                img{
                    
                    width: 300px;
                    display: block;margin: 50px auto;
                }
                p{
                    font-size: 20px !important;
                }
            }
            .infos{
                width: 70vw;
                align-items: center;
                p{
                    text-align: center;
                    font-size: 16px;

                }
                h1{
                    font-size: 80px;
                }
                
            }
        }
    }
    @media only screen and (max-width: 500px) {
        .allContent{

        }
    }

</style>