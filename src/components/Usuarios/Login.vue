<template>
    <section class="hero is-fullheight fondo">
       
        <div class="hero-body">
           
            <div class="container">
        <p class="title is-4 has-text-weight-bold has-text-white has-text-centered titulo">
        <br>
            <b-icon
                icon=""
                size=""
                >
            </b-icon>
        
        </p> 
            <div class="columns is-centered">
                <div class="column is-3-tablet is-3-desktop is-4-widescreen" >
                <form action="" class="box">
                    <div class="border p-4 rounded">
                    <img src="@/assets/logo_principal.png" alt="" height="140" width="140" style="display: block; margin:0 auto;">
                    <p class="title is-5 has-text-centered">Inicio de Sesión</p>
                    <p class="title is-3 has-text-centered"></p>
                    <label for="correo" class="form-label">Correo Electrónico</label>
                    <b-field>
                        <b-input placeholder="Correo electrónico"
                            type="email"
                            icon="email"
                            v-model="correo">
                        </b-input>
                    </b-field>
                    <label for="correo" class="form-label">Contraseña</label>
                    <b-field>
                        <b-input type="password"
                            icon="key"
                            placeholder="Contraseña"
                            v-model="password"
                            password-reveal>
                        </b-input>
                    </b-field></div>

                    <div class="field has-text-centered">
                    <b-button icon-left="login" type="is-primary" size="is-medium" @click="ingresar">Ingresar</b-button>
                    </div>
                    <p class="title is-7 has-text-centered">Cel: 937276903 / 993-845-869</p>
                    <div class="col-md-12 has-text-centered"><a href="https://cyosistemas.000webhostapp.com/">C&O - PÁGINA WEB</a></div>
                </form>
                </div>
            </div>        
            <b-loading :is-full-page="true" v-model="cargando" :can-cancel="false"></b-loading>
            </div>
        </div>
    </section>
</template>
<script>
import HttpService from '../../Servicios/HttpService'

export default {
    name: "Login",

    data: () => ({
        correo: "", 
        password: "",
        cargando:false
    }),

    methods: {
        ingresar(){
            if(!this.correo) {
                this.$buefy.toast.open({
                    message: 'Debes colocar el correo',
                    type: 'is-warning'
                })
                return
            }
            if(!this.password) {
                this.$buefy.toast.open({
                    message: 'Debes colocar la contraseña',
                    type: 'is-warning'
                })
                return
            }
            this.cargando = true
            let payload = {
                correo: this.correo,
                password: this.password
            }

            HttpService.obtenerConDatos(payload, "iniciar_sesion.php")
            .then(log => {
                if(log.resultado === "cambia"){
                   this.$buefy.toast.open({
                        message: 'Datos correctos. Debes cambiar tu contraseña',
                        type: 'is-info'
                    })
                    this.$emit("logeado", log)
                    this.cargando = false
                    return 
                }

                if(log.resultado) {
                    this.$buefy.toast.open({
                        message: 'Datos correctos. Bienvenido',
                        type: 'is-success'
                    })
                    this.$emit("logeado", log)
                    this.cargando = false
                } else {
                    this.$buefy.toast.open({
                        message: 'Datos incorrectos. Verifica tu información',
                        type: 'is-danger'
                    })
                    this.cargando = false
                }
            })
            
        }
    }

}
</script>
<style>

 @import url('https://fonts.googleapis.com/css?family=Amaranth');
.fondo {
background-color: #182a3f;
background-image: url("fondolog.png");   
background-attachment: fixed;
background-size: cover;
}
.fondo2 {
background-color: #182a3f;  
background-attachment: fixed;
background-size: cover;
}

   
.titulo{
    font-family: Amaranth, sans-serif;
    text-align: center;
    font-size: 75px;
    letter-spacing: 2px;
    word-spacing: 3px;
    color: rgb(245, 251, 255);
    text-shadow: rgb(0, 0, 0) -4px 2px 2px;
}

</style>