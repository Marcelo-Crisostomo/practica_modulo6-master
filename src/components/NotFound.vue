<template>
    <div id="NotFound">
        <h1>404 - Page Not Found</h1>
        <p>Página no encontrada</p>
        <img src="../assets/404.png" alt="404" class="error404">
        <br><br>
        
        <router-link to="/" class="volver"><i class="fa-solid fa-rotate-left"></i> Volver</router-link>   
    </div>
     
</template>

<script>
    export default{
        name:'NotFound',
        data:function(){
            return{

            }
        },
        methods:{

        }
    }
</script>

<style scoped>
    #NotFound{
        background-image: url('../assets/fondo.jpg');
        background-size: cover;
        background-repeat: no-repeat;
        /*background-color: darksalmon;*/
        height: 600px;
        color: whitesmoke;
        
    }

    .error404{
        width: auto;
        height: 400px;
    }   



    .volver{
        color: whitesmoke;
    }
</style>