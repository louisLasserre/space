<template>
  Destination view
    <section class="Dest"></section>

    <section class="allContent" v-if="activeOne">
        <div class="planet" style="">
            <article class="pageTitle"><p>01</p><p>PICK YOUR DESTINATION</p></article>
            <img :src="src" alt="">
            <!--<img src="../assets/destination/image-moon.png" alt="">-->
        </div>
        <div class="infos">
            <div class="infosbar">

                <div class="planetName" v-for="dest in destination" :key="dest.name"> 
                    <p @click="active(dest), pBorder(dest)" :class="dest.name">{{ dest.name }}</p>
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
            
            
            this.activeOne = id
            var url = id.images.png
            this.src = require("@/assets/destination/"+url)

            
            

        },
        pBorder(id){
            const p = document.getElementsByClassName(id.name)
            p[0].style.borderBottom = "3px solid white"
            p[0].style.color = "white"
            

            this.destination.forEach(dest => {
                
                if(this.activeOne.name != dest.name){
                    
                    let pp = document.getElementsByClassName(dest.name)
                    pp[0].style.borderBottom = "3px solid rgba(255, 255, 255, 0)"
                    pp[0].style.color = "#D0D6F9"
                }

                
            });
        }
        
    },
    mounted(){
    
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

        fetch('https://spacedblouis.herokuapp.com/destinations')
            .then(res => res.json())
            .then(data => {
                this.destination = data
                this.activeOne = data[0]
                
            })
            .then(() => {
                var url = this.activeOne.images.png
                this.src = require("@/assets/destination/"+url)
                this.pBorder(this.activeOne)
            })
            .catch(err => console.log(err.message))

            
        

        
    },
    
    

}
</script>

<style lang="scss">
    .pageTitle{
        width: fit-content;
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
                p{
                    border-bottom: 3px solid rgba(255, 255, 255, 0);
                    height: 40px;
                    cursor: pointer;
                    transition:  0.3s;
                }
                p:hover{
                    border-bottom: 3px solid rgba(255, 255, 255, 0.5) !important;
                    
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
                    font-size: 38px !important;
                }
                & :first-child{
                    margin-right: 60px;
                }

            }
        }
    }
    //tablet
    @media only screen and (max-width: 770px) {
        .Dest{
            background-image: url("../assets/destination/background-destination-tablet.jpg");
        }
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
        .Dest{
            background-image: url("../assets/destination/background-destination-mobile.jpg");
        }
        .planetName{
            p{
                margin-top: 0 !important;
            }
        }
        .allContent{
            padding: 0 20px; 
            .planet{
                align-items: center;
                p{
                    font-size: 16px !important;
                }
                img{
                    width: 170px;
                }
            }
            .infos{
                margin-top: 0;
                width: 100%;
                .infoNbr{
                    justify-content: space-between;
                    div{
                        text-align: center;
                    }
                    p{
                        margin: 0 !important;
                    }
                    h3{
                        font-size: 28px !important;
                        margin: 0 !important;
                        width: fit-content;
                    }
                }
            }
        }
    }

</style>