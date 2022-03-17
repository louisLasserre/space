<template>
  Crew view
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
  },
  data() {
      return {
          boucle: true,

      }
  },
  methods: {
      reload() {
          console.log("reload")
      }
  },
  mounted() {
      
  }

}
</script>

<style>

</style>