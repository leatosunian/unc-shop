<template>
    <div >
        <section class="hero productMargin">
            <div class="container">
            <!-- Breadcrumbs -->
            <ol class="breadcrumb justify-content-center">
                <li class="breadcrumb-item"><router-link to="/">Inicio</router-link></li>
                <li class="breadcrumb-item active">Estado de compra</li>
            </ol>
            
            </div>
        </section>
        <div style="display:flex; flex-direction:column; justify-content:center; align-items:center; gap:30px; margin-top:40px; margin-bottom:50vh;">
            <img :src="status.icon" alt="icon" style="width: 100px;height: 100px;" v-if="isAddress">
            <h1 v-if="isAddress">{{ status.title }}</h1>
            <h1 v-if="!isAddress">{{ submsm_error }} </h1>
            <h2 v-if="!isAddress">{{ msm_error }} </h2>
            <p style="font-size:20px" v-if="isAddress">{{ status.subtitle }} </p>
            <template v-if="validSale">
                <div>
                    <span style="font-weight:500; font-size:18px">Redirigiendo al detalle de compra</span>

                    <div class="row">
                        <div class="text-center col-12">
                            <div class="mt-4 mb-5 spinner-border" role="status">
                            <span class="visually-hidden">Cargando...</span>
                            </div>
                        </div>
                    </div> 
                </div>
            </template>
            <router-link v-if="!validSale" to="/" class="btnAdd" style="padding: 11px 26px !important;" >Volver al inicio</router-link>
        </div>
        
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'VerificationStatus',
    data(){
        return {
            status: {
                title: '',
                subtitle: '',
                icon: ''
            },
            payment_id: '',
            payment: {},
            address: '',    
            msm_error: '', 
            submsm_error: '',
            isAddress: true,
            sale: {},
            saleDetail: [],
            total: 0,
            cart: [],
            validSale: true
        }
    },
    mounted(){
        window.scrollTo(0, 0)
    },
    beforeMount(){
        this.payment_id = this.$route.query.payment_id 
        this.sale.transaction = this.payment_id 

        if(this.$route.params.address){
            this.address = this.$route.params.address
            this.sale.address = this.address
            this.isAddress = true
        } else{
            this.isAddress = false
            this.msm_error = 'No se obtuvo un domicilio de envío'
            this.submsm_error = 'Error'
        }
        
        if(this.$route.params.status == 'success'){
            this.status.title = "Pago aprobado"
            this.status.subtitle = '¡El pago ha sido efectuado correctamente!'
            this.status.icon = '/assets/icons/checked.png'
            this.getSale(this.payment_id)
        }
        if(this.$route.params.status === 'pending'){
            this.status.title = 'Pendiente de pago'
            this.status.subtitle = 'Mercado Pago está procesando tu pago. No te preocupes, en unas horas te avisaremos por e-mail si se acreditó.'
            this.status.icon = '/assets/icons/pending.png'
            this.validSale = false
            this.isAddress = true
        }
        if(this.$route.params.status === 'failure'){
            this.status.title = "Pago rechazado"
            this.status.subtitle = 'El pago no pudo ser efectuado.'
            this.status.icon = '/assets/icons/cancel.png'
            this.validSale = false
            this.isAddress = true
        }
        
     },
    methods: {
        getSale(payment_id){
            const token = localStorage.getItem('token_shopuser')
            axios.get(this.$url+'/sales/get/'+payment_id, {
                headers: {
                    "Content-Type": 'application/json',
                    "Authorization" : `Bearer ${token}`
                }
            }).then((response) => {
              const {data} = response
              console.log(data)
              setTimeout(() => {
                this.$router.push({name: 'order', params: {id:data[0]._id}})
              }, 3000);
            }).catch( error => {
              console.log(error.response.data.msg)
            }) 
        },
    }
}
</script>