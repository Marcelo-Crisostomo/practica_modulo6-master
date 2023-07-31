<template>
    <div id="OpinionesView">
        <h2>Comentarios de los Juegos</h2>
        <p>Escribe tu opinión acerca del juego: </p><p class="fw-bolder">{{ nombre }}</p>
        <hr>
        <div class="container" id="divForm">
            <form>
                <div class="mb-3">
                    <label for="txtNombre" class="form-label">Nombre:</label>
                    <input type="text" class="form-control" id="txtNombre" v-model="nombreEnviado" aria-describedby="textNombreHelp">
                    <div id="txtNombreHelp" class="form-text">Ingrese su nombre para la opinión.</div>
                </div>
                <div class="mb-3">
                    <label for="txtOpinion" class="form-label">Opinion:</label>
                    <input type="text" class="form-control" id="txtOpinion" v-model="opinionEnviada">
                </div>
                <button type="submit" v-on:click.prevent="agregarOpinion()" class="btn btn-success">{{nombreBoton}}</button>
            </form>
        </div>
        <hr>
        <h3>A continuación podras ver tu opinión</h3>
        <div class="container" id="sinOpiniones" v-if="cantidadOpiniones<1">
            <p></p>
            <p>No existen opiniones para mostrar</p>
        </div>

        <div class="accordion" id="accordionExample" v-if="cantidadOpiniones>0">
            <div class="accordion-item" v-for="(elemento,index) in opiniones">
                <h2 class="accordion-header">
                <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="collapseOne" aria-expanded="true" aria-controls="collapseOne">
                    Opinion creada por: {{ elemento.nombre }}
                </button>
                </h2>
                <div id="collapseOne" class="accordion-collapse collapse show" data-bs-parent="#accordionExample">
                    <div class="accordion-body">
                        {{ elemento.opinion }}
                    </div>
                    <button class="btn btn-danger" v-on:click="eliminarOpinion(index)">Eliminar</button>
                    <button class="btn btn-warning" v-on:click="editarOpinion(index)">Editar</button>
                </div>
                
            </div>
        </div>
        <br>
        <router-link to="/">Volver</router-link>
    </div>

</template>

<script>
    export default{
        name:'OpinionesView',
        props:['nombre'],
        data: function(){
            return{
                cantidadOpiniones:0,
                nombreEnviado: '',
                opinionEnviada:'',
                opiniones:[],
                nombreBoton:'Agregar',
                indiceActualizar:0,
            }
        },
        methods:{
            agregarOpinion: function(){
                if(this.nombreBoton == 'Agregar'){
                    this.cantidadOpiniones++;
                    let nuevaOpinion={
                        nombre:this.nombreEnviado,
                        opinion:this.opinionEnviada,
                    };
                    this.opiniones.push(nuevaOpinion);
                    this.nombreEnviado='';
                    this.opinionEnviada='';
                }
                else if(this.nombreBoton == 'Actualizar'){
                    let opinionActualizada={
                        nombre:this.nombreEnviado,
                        opinion:this.opinionEnviada,
                    };
                    this.opiniones.splice(this.indiceActualizar,1, opinionActualizada);
                    alert('La opinión fue actualizada. Revise el acordeon con la nueva información');
                }


                
            },
            eliminarOpinion:function(indice){
                this.cantidadOpiniones--;
                this.opiniones.splice(indice,1);
            },
            editarOpinion:function(indice){
                this.nombreEnviado=this.opiniones[indice].nombre;
                this.opinionEnviada=this.opiniones[indice].opinion;
                this.nombreBoton = 'Actualizar';
                this.indiceActualizar = indice;
                alert('Va a editar una opinión. Revise el formulario con la información cargada');
            },
        }
    }
</script>

<style scoped>
    #OpinionesView{
        background-color:#020202;
        height: 87vh;
        color:#fff;
    }
    
    #divForm{
        background-color: whitesmoke;
        text-align: start;
        color: #020202;
        padding: 30px;
        border-radius: 10px;
    }

    #sinOpiniones{
        padding: 20px;
        background-color:#0D2818;
        color: #fff;
        justify-content: center;
        text-align: start;
        border-radius: 10px;
    }
</style>