<template>
    <section  style="padding-top: 3em;  bottom: 0;">
        <footer class="footer is-primary fondo2">   
            <div >
                 <span class="is-pulled-right has-text-white">
                    <img src="@/assets/logo.png" alt="logo" width="400" height="400">   
                </span>
                <p class="titulo content has-text-centered title is-4 has-text-white">
                    <strong>Empresa: {{ datosLocal. nombre }}</strong> / Celular: <strong>{{ datosLocal.telefono }}</strong>
                </p>  
            </div>

        </footer>
    </section>
</template>
<script>
import HttpService from '../Servicios/HttpService'
export default {
    name: "Pie",

    data: () =>({
        datosLocal: {}
    }),

    mounted(){
        this.obtenerDatos()
    },

    methods: {
        obtenerDatos(){
            HttpService.obtener("obtener_datos_local.php")
            .then(resultado => {
                this.datosLocal = resultado
            })
        }
    }
}
</script>
