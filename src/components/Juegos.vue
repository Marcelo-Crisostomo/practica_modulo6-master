<template>
    <div id="Juegos">
        <h1 class="tituloH1">Listado de Juegos</h1>
        <br>
        <div class="contenedorPadre">
            <div v-for="(juego,index) in juegos" v-bind:key="index" class="card m-3" style="width: 18rem;">
                <img v-bind:src="juego.background_image" class="card-img-top" alt="logo" height="160">
                <div class="card-body">
                    <h5 class="card-title">{{juego.name}}</h5>
                    <p class="card-text">ESRB Rating: {{ juego.esrb_rating.name }}</p>
                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Rating: {{ juego.rating }}</li>
                    <li class="list-group-item">Released: {{ juego.released }}</li>
                    <li class="list-group-item">Updated: {{ juego.updated }}</li>
                </ul>
                <div class="card-body">
                    <a v-on:click="mostrarOpiniones(juego.name)" class="btn btn-success">Opinar</a>
                    <a v-on:click="irAdministracion(juego.name)" class="btn btnColor"><i class="fa-solid fa-heart"></i></a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    import axios from 'axios';
    export default{
        name: 'Juegos',
        data: function(){
            return{
                cantidadJuegos:0,
                juegos:[],
            }
        },
        methods: {
            consumirApi: function(){
                let url='https://api.rawg.io/api/games?key=0ec7e270048d439dac9b19b316e6a25e';
                axios(url)
                .then(respuesta => {
                    this.cantidadJuegos = respuesta.data.results.length;

                    //logica para acumular en el arreglo juego cada juegos de las distintas paginas
                    for(let i=0; i < this.cantidadJuegos; i++){
                        this.juegos.push(respuesta.data.results[i]);
                    } 
                })
                .catch(error => {
                    console.log(error);
                });
            },

            mostrarOpiniones:function(nombreJuego){
                this.$router.push(`/opiniones/${nombreJuego}`);
            },
            irAdministracion:function(nombreJuego){
                this.$router.push(`/administracion/${nombreJuego}`);
            }

        },

        created(){
            this.consumirApi();
        }
    }
</script>

<style scoped>
    #Juegos{
        background-color: #020202;
        background-size: contain;
    }

    .contenedorPadre {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        padding: 50px 0px 100px;
    }

    .btnColor{
        color: #16db65;
        font-size: 25px;
    }

    .tituloH1{
        padding-top: 50px;
        color: whitesmoke;
        font-weight: bold;
    }
    .btn-success{
        background-color: #058C42;
        border-color: #058C42;
    }
</style>