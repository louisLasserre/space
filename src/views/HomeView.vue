<template>
  <section class="home"></section>
    <div class="content">
      <article class="Hometext">
        <h3>SO, YOU WANT TO TRAVEL TO</h3>
        <h1>SPACE</h1>
        <p>
        Let’s face it; if you want to go to space, you might as well genuinely go to
        outer space and not hover kind of on the edge of it. Well sit back, and relax
        because we’ll give you a truly out of this world experience!</p>
      </article>
      <router-link to="destination">
        <div class="circle"><div class="innerCircle"></div><h1>EXPLORE</h1></div>
      </router-link>



    </div>


</template>

<script>
// @ is an alias to /src


export default {
  name: 'HomeView',
  data() {
    return {

    }
  },
  mounted(){

    const border = document.getElementsByClassName('border')

    var width =  document.body.clientWidth
    if(width <= 770 && width > 500 ){
      console.log("tablet")
      border.border.style.left = '14%'
      border.border.style.width = '40px'

    }else if(width <= 500){
      console.log("mobile")
      border.border.style.left = '14%'
      border.border.style.width = '40px'

    }else{
      console.log("pc")
      border.border.style.left = '14.5%'
      border.border.style.width = '60px'
    }



  }
}
</script>

<style lang="scss">

  .home{

    position: absolute;left: 0;right: 0;bottom: 0;top: 0;

    z-index: 0;
    background-image: url('../assets/home/background-home-desktop.jpg');
    background-repeat: no-repeat;
    background-size: cover;
  }
  .content{
    margin: 0 165px 100px 165px;

    position: fixed;bottom: 0;left: 0;right: 0;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    .circle{

      width: 274px;
      height: 274px;
      border-radius: 50%;
      background: white;
      position: relative;
      text-align: center;
      z-index: 2;
      &:hover .innerCircle{
        width: 450px;
        height: 450px;
      }
      .innerCircle{
        width: 270px;
        height: 270px;
        transition-duration: 0.5s ;//not working
        background: rgba(255, 255, 255, 0.116);
        border-radius: 50%;
        position: absolute;left: 50%;top: 50%;
        transform: translate(-50%, -50%);

        z-index: 1;
      }
      h1{
        font-size: 32px;
        color: black;
        position: absolute;
        top: 50%;left: 50%;
        transform: translate(-50%, -50%)

      }
    }
    a{
      text-decoration: none;
    }
  }
  .Hometext{
    text-align: left;
    width: 450px;
    h1{
      margin: 20px 0;
    }
    p{
      line-height: 32px;
    }



  }
@media only screen and (max-width: 770px) {
  .content{
    flex-direction: column;
    align-items: center;

    position: relative;
    margin: 10vh auto 0 auto ;

    .circle{
      margin-top: 15vh;
      width: 242px;height: 242px;
      .innerCircle{display: none;}
    }
    .Hometext{
      text-align: center;
    }
  }
  .home{
    background-image: url("../assets/home/background-home-tablet.jpg");
  }


}
@media only screen and (max-width: 500px) {
  .home{

    background-image: url("../assets/home/background-home-mobile.jpg");
  }
  .content{
    width: 80vw;
    .circle{
      width: 160px;
      height: 160px;
      h1{
        font-size: 20px;
      }
      .innerCircle{
        display: none;
      }
    }
  }
  .Hometext{
    width: 100%;
    h1{
      font-size: 80px;
    }
    h3{
      font-size: 16px;
    }
    p{
      font-size: 15px;
    }
  }
}
</style>
