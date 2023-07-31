<template>
    <div id="Administracion">
        <div id="adminHijo">
            <h2>Resumen de tu Cuenta</h2>
            <hr>
        <div v-if="flagButton">
            <button class="btn btn-success" v-on:click="mostrarFormulario">Ingresar Datos</button>
        </div>

        <div v-if="flagForm" class="container">
            <form>
                <div class="mb-3">
                    <label for="txtNombre" class="form-label">Nombre:</label>
                    <input type="text" class="form-control" id="txtNombre" v-model="nombreEnviado" aria-describedby="textNombreHelp">
                    <div id="txtNombreHelp" class="form-text">Ingrese su nombre para la opinión.</div>
                </div>
                <div class="mb-3">
                    <label for="txtApellido" class="form-label">Apellido:</label>
                    <input type="text" class="form-control" id="txtApellido" v-model="apellidoEnviado">
                </div>
                <button type="submit" v-on:click.prevent="enviarDatos()" class="btn btn-info">Enviar</button>
            </form>
        </div>

        <div v-if="flagResumen" class="container">
            <div class="row">
                <div id="seccionNombre" class="col-md-2">
                    <p>Bienvenid@</p>
                    <p class="nombres">{{ nombreEnviado }} {{ apellidoEnviado }}</p>
                </div>
                <div class="col-md-1">

                </div>
                <div class="col-md-6">
                    <div class="container">
                        <div class="row">
                            <div class="col-m-12">
                                <h4>Le diste me gusta al juego:</h4>
                                <h3 class="nombres"> {{ nombre }} </h3>
                            </div>
                        </div>
                        <hr>
                        <div class="row">
                            <div class="col-md-12 borde">
                                <div id="divCoins" class="container text-center">
                                    <p>¿Deseas comprar Coins para este Juegos?</p>
                                    <button id="btnCoins" class="btn btn-warning" v-on:click="agregarCoins()"><i class="fa-solid fa-coins" label="Agregar"></i> Agregar coins</button>
                                    <br><br>
                                    <p>Cantidad de Coins Comprados</p>
                                    <div class="progress" role="progressbar" aria-label="Example with label" v-bind:aria-valuenow="cantidadCoins" aria-valuemin="0" aria-valuemax="100">
                                        <div class="progress-bar bg-success" style="width: 0%">${{cantidadCoins}}</div>
                                    </div>
                                    <div v-if="flagMaximo">
                                        <p class="text-danger">LLegaste al máximo de tu crédito</p>
                                    </div>
                                    <br>
                                </div>
                            </div>
                        </div>
                        <hr>
                    
                    </div>

                    <div class="col-md-3">

                    </div>
                    
                    <div class="row">
                            <div class="col-md-4 bg-warning">
                                <p class="letras">% de finalización de juego</p>
                                <hr>
                                <p class="letras">17% <i class="fa-regular fa-star-half"></i></p>
                            </div>
                            <div class="col-md-4 bg-success">
                                <p class="letrasLogros">Logros en el juego</p>
                                <hr>
                                <p class="letrasLogros">166 <i class="fa-solid fa-trophy"></i></p>
                            </div>
                            <div class="col-md-4 bg-info">
                                <p class="letras">Recompensas</p>
                                <hr>
                                <p class="letras">200 <i class="fa-solid fa-award"></i></p>
                            </div>
                </div>

                    
                    
                </div>
                

            </div>
            
            
        </div>

        </div>
        
        
    </div>
    <br>
    <router-link to="/">Volver</router-link>
</template>

<script>
    export default{
        name:'Administracion',
        props:['nombre'],
        data: function(){
            return{
                flagButton:true,
                flagResumen:false,
                flagMaximo:false,
                flagForm:false,
                nombreEnviado:'',
                apellidoEnviado:'',
                cantidadCoins:0,

            }
        },
        methods:{
            mostrarFormulario:function(){
                this.flagButton= false;
                this.flagForm=true;
            },

            enviarDatos:function(){
                this.flagForm=false;
                this.flagResumen=true;
            },
            agregarCoins:function(){
                this.cantidadCoins++;
                let laBarra = document.getElementsByClassName('progress-bar');
                let valorPorCiento = '';
                if (this.cantidadCoins<50){
                    valorPorCiento = `${this.cantidadCoins}%`;
                    laBarra[0].style.width = valorPorCiento;
                    if(this.cantidadCoins>20 && this.cantidadCoins<=30){
                        laBarra[0].classList.remove('bg-success');
                        laBarra[0].classList.add('bg-warning');
                    }
                    else if(this.cantidadCoins>30){
                        laBarra[0].classList.remove('bg-warning');
                        laBarra[0].classList.add('bg-danger');
                    }
                }else{
                    this.flagMaximo = true;
                    let elBotonCoins = document.getElementById('btnCoins');
                    elBotonCoins.setAttribute('disabled', true);
                }
            },
        }
    }
</script>

<style scoped>

    #Administracion{
        background-color:#020202;
        background-size: cover;
       
    }

    #adminHijo{
        background-color: whitesmoke;
        padding-bottom: 20px;
    }

    #seccionNombre{
        background-color: black;
        color: white;
    }

    .letras{
        font-size: 20px;
    }

    .letrasLogros{
        font-size: 20px;
        color: white;
    }

    .nombres{
        font-weight: bold;
    }

    .borde{
        border: 1px solid lightgray;
    }
</style>