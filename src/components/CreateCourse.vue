<template>
  <div class="col-12 col-sm-10 col-md-8 offset-sm-1 offset-md-2">
    <div class="mt-5">
      <form class="border border-primary rounded form-inline" @submit.prevent="createCourse">

        <h2 class="col-12 text-center text-primary mt-3 mb-5">Crear un curso</h2>

        <div class="form-group col-12">
              <label class="custom-label col-md-3" for="courseName">Curso</label>
              <input id="courseName" class="form-control col-12 col-sm-10 col-md-7 offset-sm-1" type="text"
              placeholder="Curso" v-model="courseName" required/>
        </div>

        <div class="form-group col-12">
              <label class="custom-label col-md-3" for="durationHours">Intensidad Horaria</label>
              <input id="durationHours" class="form-control col-12 col-sm-10 col-md-7 offset-sm-1" type="number"
              placeholder="Intensidad Horaria" v-model="durationHours" required/>
        </div>

        <div class="col-12 mb-3">
          <button class="col-sm-6 col-md-4 offset-sm-5 offset-md-7 btn btn-primary" type="submit">
            Crear Curso
          </button>
        </div>

      </form>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  const path = "/principal/profesor/crear-curso/";

  export default {
    name: "CreateCourse",
    data( ){
      return {
        courseName: '',
        durationHours: '',
      }
    },
    methods: {
            createCourse( event ){
                axios
                .post( this.$store.state.backURL + path + this.role, // URL
                      {
                      courseName: this.courseName,
                      durationHours: this.durationHours
                      }                   
                ).then( response => {
                    if( response.status !== 200 ){
                        alert( "Error en la creación del curso" );
                    }else{
                        alert( "Curso creado con éxito" )
                    }
                } ).catch( error => {
                    if( error.response.status === 400 ){
                      alert( "Error" );
                    }else{
                      alert( "¡Parece que hubo un error de comunicación con el servidor!" );
                    }
                } );

                event.preventDefault();
            }
        }
    }
  
</script>

<style scoped>
  .form-inline .form-group{
    margin-bottom: 1rem;
  }
</style>
