<template>
  technology
</template>

<script>
export default {
    mounted(){
    
        const border = document.getElementsByClassName('border')
    
        var width =  document.body.clientWidth
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
  }

}
</script>

<style>

</style>