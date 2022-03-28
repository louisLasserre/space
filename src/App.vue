<template>
  <header>
    <div class="svg">

      <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48"><g fill="none" fill-rule="evenodd"><circle cx="24" cy="24" r="24" fill="#FFF"/><path fill="#0B0D17" d="M24 0c0 16-8 24-24 24 15.718.114 23.718 8.114 24 24 0-16 8-24 24-24-16 0-24-8-24-24z"/></g></svg>
    </div>
    <nav class="nav">
      <router-link @click="close" to="/"><p class="nbr"><strong>00</strong></p><p>HOME</p></router-link> 
      <svg class="trait" width="473" height="1" viewBox="0 0 473 1" fill="none" xmlns="http://www.w3.org/2000/svg">
      <rect opacity="0.251485" width="473" height="1" fill="white"/>
      </svg>
      <router-link @click="close" to="/destination"><p class="nbr"><strong>01</strong></p><p>DESTINATION</p></router-link> 
      <router-link @click="close" to="/crew"><p class="nbr"><strong>02</strong></p><p>CREW</p></router-link>
      <div class="border" id="border" ref="border"></div>
      <svg class="croix" @click="close" xmlns="http://www.w3.org/2000/svg" width="20" height="21"><g fill="#D0D6F9" fill-rule="evenodd"><path d="M2.575.954l16.97 16.97-2.12 2.122L.455 3.076z"/><path d="M.454 17.925L17.424.955l2.122 2.12-16.97 16.97z"/></g></svg>
      <router-link @click="close" to="/technology"><p class="nbr"><strong>03</strong></p><p>TECHNOLOGY</p></router-link> 
      

    </nav>
    <svg class="hamb" @click="open" xmlns="http://www.w3.org/2000/svg" width="24" height="21"><g fill="#D0D6F9" fill-rule="evenodd"><path d="M0 0h24v3H0zM0 9h24v3H0zM0 18h24v3H0z"/></g></svg>
  </header>
  <router-view/>
</template>


<script>



export default{
  methods: {
    close() {
      var width =  document.body.clientWidth
      if (width < 500){
        const nav = document.getElementsByClassName("nav")
        nav[0].style.width = '0px'
        nav[0].style.paddingLeft = '0px'
        nav[0].style.paddingRight = '0px'
      }
    },
    open() {
      const nav = document.getElementsByClassName("nav")
      nav[0].style.width = '60vw'
      nav[0].style.paddingLeft = '40px'
      
    }
    
  },
  
  
}
</script>


<style lang="scss">
$height: 30px;
$text: white;

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body{
  
  background: black;
  
  background-repeat: no-repeat;
  background-size: cover;
  
  p{
    font-family: 'Barlow Condensed', sans-serif !important;
    font-size: 16px;
    margin: 0;
    color: $text;
    

  }
  h1, h3{
    color: $text;
    
    margin: 0;
    font-weight: 400;
    
  }
  h1{
    font-size: 150px;
    font-family: 'Bellefair', serif !important;
  }
  h3{
    font-size: 28px;
    font-family: 'Barlow Condensed', sans-serif;
  }
  
  strong{
    font-weight: 700;
  }
  margin: 0;
}
header{
  margin-top: 45px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 10;
  position: relative;

  svg{
    display: block;
    margin: 0 auto;
  }
  .svg{
    width: 165px;

  }
  .hamb{
    display: none;
  }
}

.nav {
  padding:  $height 20px 0 20px;
  background: rgba($color: #ffffff, $alpha: 0.1);
  width: fit-content;
  
  backdrop-filter: blur(20px);
  display: flex;
  align-items: center;
  transition: all 0.4s ease;

  //
  position: relative;
  
  .croix{
    display: none;
  }

  svg{
    position: absolute;
    left: 0;top: 50%;
    transform: translateX(-95%);
    
    
  }
  a{
    
    color: #ffffff;
    margin: 0 35px;
    display: flex;
    height: fit-content;
    text-decoration: none;
    padding-top: 3px;
    padding-bottom: $height;

    border-bottom: 3px solid rgba(255, 255, 255, 0);
    
    p:first-child{
      margin-right: 5px;
    }

    // &.router-link-exact-active {
    //   border-bottom: 3px solid white;
    // }
    &:hover{
      border-bottom: 3px solid rgba(255, 255, 255, 0.521);
    }
  }
  a:last-child{
    margin-right: 165px;
  }
  a:first-child{
    margin-left: 100px;
  }
  .border{
    position: absolute;bottom: 0;
    height: 3px;
    background: rgb(255, 255, 255);
    width: 70px;
    transition: all 0.3s ease-out;
  }
  
}
@media only screen and (max-width: 770px) {
  .trait{
    display: none;
  }
  header{
    margin-top: 0;
    svg{
      margin-left: 39px;
    }
  }
  .nav{
    backdrop-filter: none;
    a:last-child{
      margin-right: 39px;
    }
    a:first-child{
      margin-left: 48px;
    }
    a{
      margin: 0 20px;
    
    }
  }
  .nbr{
    display: none;
  }
}
@media only screen and (max-width: 500px) {
  .nav{
    width: 0vw;
    padding-left: 0px;
    padding-right: 0px;
   


    height: 100vh;
    z-index: 5;
    backdrop-filter: blur(50px);
    
    overflow-x: hidden;
    position: fixed;top:0;right:0;
    flex-direction: column;
    align-items: flex-start;
    text-align: left;
    
    a{
      margin: 0 !important;
    }
    a:first-child{
      margin-top: 10vh !important;
    }
    .border{
      display: none;
    }
    .nbr{
      display: inline;
      margin-right: 20px !important;
    }
    .croix{
      display: block;
      position: absolute;
      padding: 20px;
      top: 20px;
      left: 77%;
    }
  }

  header{
    .hamb{
      display: block;
      margin: 0 39px 0 0 ;
      padding: 20px;
    }
    margin-top: 20px;
  }
  
}
</style>
