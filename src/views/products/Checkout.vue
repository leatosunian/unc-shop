<template>
    <div >
        <!-- Hero Section-->
        <section class="hero productMargin">
            <div class="container">
            <!-- Breadcrumbs -->
            <ol class="breadcrumb justify-content-center">
                <li class="breadcrumb-item"><router-link to="/">Inicio</router-link></li>
                <li class="breadcrumb-item active">Resumen de compra</li>
            </ol>
            <!-- Hero Content-->
            <div class="pb-5 text-center hero-content">
                <h1 class="hero-heading">Resumen de compra</h1>
                <div class="row">   
                    <div class="col-xl-8 offset-xl-2">
                        <p class="lead text-muted">Por favor, revisá tu orden.</p>
                    </div>
                </div>
            </div>
            </div>
        </section>

        <section v-if="cart.length === 0">
            <div class="container">
                <div class="row">

                    <div class="col-lg-8 col-xl-9"  style="margin: 0 auto; margin-bottom: 500px;">
                        <div class="card" style="">
                            <div class="card-body">
                            <div class="row" >
                                <div class="text-center col-12">
                                <img src="../../../public/assets/icons/cart0.png" style="width:90px; height:90px; margin-bottom:35px" alt="">
                                <h3 style="font-size:24px;">No tenés productos en tu carrito.</h3>
                                <span style="color:black;font-weight:400;font-size:17px;">¿Que esperas para llenarlo? </span>
                                <router-link to="/products" class="textLink" style="font-weight:600;font-size:17px;margin-left:1px!important;">Ver productos</router-link>
                                </div>
                            </div>
                            </div>
                        </div>
                    </div>

                </div>
            </div>    
        </section>
    
        
        <!-- Checkout-->
        <section v-if="cart.length >= 1">
            <div class="container">
                <div class="row">
                    <div class="mb-5 "> 
                        <div class="col-lg-12">
                            <div class="cart">
                                <div class="cart-wrapper">
                                    <div class="text-center cart-header" style="border-bottom:1px solid orange;">
                                        <div class="row">
                                            <div class="col-5">Producto</div>
                                            <div class="col-2">Precio</div>
                                            <div class="col-2">Cantidad</div>
                                            <div class="col-2">Subtotal</div>
                                            <div class="col-1"></div>
                                        </div>
                                    </div>
                                    <div class="cart-body">
                                        <!-- Product-->
                                        <div class="cart-item" v-for="item in cart">
                                            <div class="text-center row d-flex align-items-center">
                                                <div class="col-5">
                                                <div class="d-flex align-items-center">
                                                    <router-link :to="/product/+item.product.slug">
                                                        <img class="cart-item-img" :src="$url+'/getImage/'+item.product.image" alt="...">
                                                    </router-link>
                                                    
                                                    <div class="cart-title text-start">
                                                        <router-link :to="/product/+item.product.slug" class="text-uppercase text-dark"><strong>{{item.product.name}}</strong>
                                                        </router-link>
                                                        <br>
                                                        <span class="text-sm text-muted">{{item.product.str_variant}}: {{item.variant.variant}}</span>
                                                    </div>
                                                </div>
                                                </div>
                                                <!-- <div class="col-2">{{priceConverter(item.product.price)}}</div> -->
                                                <div class="col-2" v-if="USDEnabled == false">{{priceConverter(item.product.price*USDData.value)}}</div>
                                                <div class="col-2" v-if="USDEnabled == true">{{priceConverter(item.product.price)}}</div>

                                                <div class="col-2">
                                                    <div class="d-flex align-items-center" style="width:100px;justify-content: center;">
                                                        <span class="" type="text">{{ item.amountOfProducts }}</span>                                        
                                                    </div>
                                                </div>

                                                <!-- <div class="text-center col-2">{{priceConverter(item.product.price*item.amountOfProducts)}}</div> -->
                                                <div class="text-center col-2" v-if="USDEnabled == false">{{priceConverter(item.product.price*USDData.value*item.amountOfProducts)}}</div>
                                                <div class="text-center col-2" v-if="USDEnabled == true">{{priceConverter(item.product.price*item.amountOfProducts)}}</div>

                                                <div class="text-center col-1">
                                                    <a class="cart-remove" v-on:click="deleteItem(item._id)">
                                                        <img src="/assets/icons/redclose.png" alt="" style="width:12px; height:12px;">
                                                    </a>
                                                </div>
                                            </div>
                                        </div>
                                        <!-- Product-->                                    
                                    </div>
                                </div>
                            </div>

                            <div class="my-2 d-flex justify-content-between flex-column flex-lg-row">
                                <router-link to="/products" class="btn btn-link">Continuar comprando</router-link>
                            </div>
                            
                        </div>
                    </div>

                    <div class="col-lg-8">
                        <div class="block mb-3">
                            <div class="block-header">
                                <h6 class="mb-0 text-uppercase">Domicilio de entrega</h6>
                            </div>

                            <div v-if="addresses.length >= 1" class="addressesCont" v-for="item in addresses">
                                <div class="">
                                    <label class="form-label" stlye="margin-bottom:0px!important;">Destinatario</label>
                                    <div style="width:fit-content; height:fit-content; border:1px solid rgba(0, 0, 0, 0.18); padding:8px 18px; border-radius: 8px; font-size:14px;">
                                        {{item.surname}}, {{item.name}}
                                    </div>
                                </div>
                                <div class="">
                                    <label class="form-label" stlye="margin-bottom:2px!important;">Domicilio </label>
                                    <div style="width:fit-content; height:fit-content; border:1px solid rgba(0, 0, 0, 0.18); padding:8px 18px; border-radius: 8px; font-size:14px;">
                                        {{item.address}}
                                    </div>
                                </div>
                                <div class="" >
                                    <label class="form-label" stlye="margin-bottom:2px!important;">Ciudad</label>
                                    <div style="display:flex; flex-direction:row; align-items:center;">
                                        <div style="width:fit-content; height:fit-content; border:1px solid rgba(0, 0, 0, 0.18); padding:8px 18px; border-radius: 8px; font-size:14px;">
                                            {{item.city}}
                                        </div>
                                        <input type="radio" name="shipping" style="margin-left:25px; width:18px; height:18px;" :value="item._id" v-on:change="selectDirection($event)">
                                    </div>
                                </div>
                            </div>

                        </div>

                        <router-link to="/profile/address" class="textLink">Gestionar mis domicilios de entrega</router-link>

                        <div class="block mt-5">
                            <div class="block-header">

                                <h6 class="mb-2 text-uppercase" >
                                    Métodos de envío 
                                    
                                </h6>
                                <button v-b-modal.modal-lg variant="primary" style="border:none; margin-top:0px; margin-left:0!important;background-color:white!important" class="textLink">
                                    Información sobre métodos de envío
                                </button>

                                <b-modal id="modal-lg" size="lg" title="Métodos de envío" >
                                  <div style="display:flex;flex-direction:column;padding:0 30px; gap:10px">
                                    <span style="font-weight:600; font-size: 18px;">
                                        - Envío a domicilio
                                        <p style="font-weight:400; font-size: 17px;">Comprá y recibí tu pedido sin moverte de tu casa dentro de las 72hs hábiles. Realizamos envíos a todo el país a través de {{ shipMethods.shippingCompany }}. Cuando despachemos el pedido te enviaremos un Nº de seguimiento para que rastrees tu orden.</p>
                                    </span>
                                    <span style="font-weight:600; font-size: 18px;">
                                        - Retirá por nuestra sucursal
                                        <p style="font-weight:400; font-size: 17px;">Podés acercarte a nuestra sucursal luego de hacer la compra y retirar tu pedido sin cargo.</p>
                                    </span>
                                  </div>
                                  <template #modal-footer>
                                    <div class="">
                                      
                   
                                    </div>
                                  </template>
                                </b-modal>
                            </div>

                            <div class="" style="display:flex; justify-content:left; width:100%;" v-if="!freeShipping">
								<div class="shipType">
                                    
                                    <div style="border: 1px solid rgba(0, 0, 0, 0.18); border-radius: 8px; padding: 6px 10px; display: flex; align-items:center; justify-content:space-between; gap:10px;">
                                        <span>Envío a domicilio</span>
                                        <input type="radio" v-model="shippingCost" v-on:click="selectShipMethod($event)" :value="shipMethods.toAddress" name="shippingMethod" id="toAddress" style="width:18px; height:18px;">
                                    </div>
                                    
                                    <div v-if="shipMethods.toBranch === 'Permitido'" style="border: 1px solid rgba(0, 0, 0, 0.18); border-radius: 8px; padding: 6px 10px; display: flex; align-items:center; justify-content:space-between; gap:10px;">
                                        <span>Retiro por nuestra sucursal</span>
                                        <input type="radio" v-model="shippingCost" v-on:click="selectShipMethod($event)" value="0" name="shippingMethod" id="toBranch" style="width:18px; height:18px;">
                                    </div>
                                 
                                </div>
                            </div>

                            <div class="" style="display:flex; justify-content:center; width:100%;" v-if="freeShipping">
							    <div style="display:flex; justify-content:left; width:100%; padding-left:24px; gap:10px">
                                    
                                    <div style="border: 1px solid rgba(0, 0, 0, 0.18); border-radius: 8px; padding: 6px 10px; display: flex; align-items:center; justify-content:space-between; gap:10px;">
                                        <span>Envío a domicilio</span>
                                        <input type="radio"  v-on:click="selectShipMethodFree($event)"  name="shippingMethod2" id="toAddress" style="width:18px; height:18px;">
                                    </div>

                                    <div v-if="shipMethods.toBranch === 'Permitido'" style="border: 1px solid rgba(0, 0, 0, 0.18); border-radius: 8px; padding: 6px 10px; display: flex; align-items:center; justify-content:space-between; gap:10px;">
                                        <span>Retiro por nuestra sucursal</span>
                                        <input type="radio"  v-on:click="selectShipMethodFree($event)" value="0" name="shippingMethod2" id="toBranch" style="width:18px; height:18px;">
                                    </div>
                                 
                                </div>
                            </div>

                        </div>


                    </div>

                    <div class="mb-6 col-lg-4" >
                        <div class="block mb-5" >
                            <div class="block-header" style="background-color:white!important">
                                <h6 class="mb-0 text-uppercase">Resumen del pedido</h6>
                            </div>
                            <div class="pt-1 block-body bg-light" style="background-color:white!important">
                                <ul class="mb-0 order-summary list-unstyled">
                                    <li class="order-summary-item">
                                        <span>Subtotal </span>
                                        <span>
                                            {{priceConverter(total)}}
                                        </span>
                                    </li>
                                    <li class="order-summary-item">
                                        <span>Envío</span>
                                        <span v-if="!freeShipping">
                                            {{priceConverter(this.shippingCost)}}
                                        </span>
                                        <span v-if="freeShipping">
                                            Gratis
                                        </span>
                                    </li>
                                    <li class="border-0 order-summary-item">
                                        <span>Total</span>
                                        <strong class="order-summary-total" v-if="this.shippingCost > 0">
                                            {{priceConverter(total + this.shippingCost)}}
                                        </strong>
                                        <strong class="order-summary-total" v-if="this.shippingCost == 0">
                                            {{priceConverter(total)}}
                                        </strong>
                                    </li>
                                </ul>
                            </div>
                            
                            
                            <div class="block mb-5" >
                                <div class="block-header" style="background-color:white!important">
                                    <h6 class="mb-0 text-uppercase">Métodos de pago</h6>
                                </div>
                                <div class="pt-1 mb-3 block-body bg-light" style="background-color:white!important">
                                    <div class="mb-2 col-md-12">
                                     
                                        <span class="mb-2 d-block" style="letter-spacing: 0px;font-weight: 600;">Tarjeta de crédito</span>
                                        <div class="row">
                                            <div class="mb-2 col-12">
                                                <img src="../../../public/assets/icons/ccreditcards.png" style="width: 360px">
                                            </div>
                                        </div>

                                        <span class="mb-2 d-block" style="letter-spacing: 0px;font-weight: 600;">Tarjeta de débito</span>
                                        <div class="row">
                                            <div class="mb-2 col-12">
                                                <img src="../../../public/assets/icons/debitcards.png" style="width: 360px">
                                            </div>
                                           
                                        </div>
                                        <span class="mb-2 d-block" style="letter-spacing: 0px;font-weight: 600;">Efectivo</span>
                                        <div class="row">
                                            <div class="mb-2 col-12">
                                                <img src="../../../public/assets/icons/cash.png" style="width: 360px">
                                            </div>
                                            <div class="col-12">
                                                <p class="text-muted" style="font-size: 13px">
                                                    (Luego de hacer clic en "Realizar compra" será redirigido a Mercado Pago  de forma segura para completar su compra).</p>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <div class="col-md-12">
                                        <p class="text-sm" style="margin-bottom: 0.4rem;">Tus datos personales serán utilizados para procesar tu pedido y respaldar tu experiencia en este sitio web.</p>
                                        <a > <b> Términos y privacidad.</b></a>
                                    </div>
                    
                                </div>
                                    <!-- ERROR ALERT -->
                                    <div class="alert" style="width:fit-content !important; height:fit-content !important; padding: 7px 14px; display: flex !important; justify-content:left !important; border-radius: 8px; margin: 0 0 !important; margin-bottom:25px !important; margin-left:23px !important;"  v-if="!valid">
                                        <small class="">{{ msm_error }} </small>
                                    </div>

                                    <button v-if="!validSale && cart.length >= 1" type="button" class="btn btn-dark"  style="margin: 0 1.5rem;" v-on:click="createSale()">Realizar compra</button>
                                    <template v-if="validSale">
                                        <div>
                                            <div class="row">
                                                <div class="text-center col-12">
                                                    <div class="mt-4 mb-5 spinner-border" role="status">
                                                    <span class="visually-hidden">Cargando...</span>
                                                    </div>
                                                </div>
                                            </div> 
                                        </div>
                                    </template>
                              </div>
                        </div>

                  
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
import axios from 'axios'
import currencyFormatter from 'currency-formatter'

export default {
    name: 'Checkout',
    data(){
        return {
            cart: [],
            loading: false,
            addresses: [],
            sell: {},
            items: [],
            shipMethods: {},
			shipMethodSelected: '',
            shippingCost: 0,
			freeShipping:false,
            total: 0,
            msm_error: '',
            valid: true,
            validSale: false,
            USDData: {},
            USDEnabled: null,
            sale: {},
            saleDetail: [],
            saleID: ''
        }
    },
    beforeMount(){
        this.getUSDSettings()
        this.getCart()
        this.getAddress()
        this.validSale = false  

    },
    mounted(){
        window.scrollTo(0, 0)
    },
    methods: {
        selectShipMethod(price){

            if(price.target.value == this.shippingCost){
                return
            } else{
                this.shippingCost = '0'
                this.shippingCost = price.target.value
            }
            
            this.shipMethodSelected = price.target.id
        },
		selectShipMethodFree(e){
			this.shipMethodSelected = e.target.id
			console.log(this.shipMethodSelected);
		},
        getCart(){          
            const token = localStorage.getItem('token_shopuser')
            if(token){
                var loader = this.$loading.show({
                    container: this.fullPage ? null : this.$refs.formContainer,
                    canCancel: false,
                    color: "orange",
                    opacity: 1
                });
            }
            const getUser = JSON.parse(localStorage.getItem('data_shopuser'))
            const user = getUser[1]

            axios.get(this.$url+'/cart/get/'+user, {
                headers: {
                    "Content-Type": 'application/json',
                    "Authorization": `Bearer ${token}`
                }
            }).then((response) => {
                this.total = 0
                const {data} = response
                this.cart = data
                this.loading = false
                loader.hide()

                for(const item of data){
                    const subtotal = item.product.price * item.amountOfProducts
                    this.total = this.total + subtotal
                    if(this.USDEnabled == false){
                        this.items.push({
                            id: item.product._id,
                            title: item.product.name,
                            description: item.product.description,
                            quantity: item.amountOfProducts,
                            currency_id: 'ARS',
                            unit_price: item.product.price * this.USDData.value, 
                        }) 
                    }
                    if(this.USDEnabled == true){
                        this.items.push({
                            id: item.product._id,
                            title: item.product.name,
                            description: item.product.description,
                            quantity: item.amountOfProducts,
                            currency_id: 'ARS',
                            unit_price: item.product.price, 
                        }) 
                    }

                    this.saleDetail.push({
                        subtotal: subtotal,
                        unitPrice: item.product.price,
                        items: item.amountOfProducts,
                        client: user,
                        product: item.product._id,
                        variant: item.variant._id
                    })
                }

                if(this.USDEnabled == false){
                    this.total = this.total * this.USDData.value
                }

                this.sale.total = this.total
                this.sale.client = user
                this.getShippingMethods()

            }).catch( error => {
                console.log(error.response.data.msg)
                this.msm_error = error.response.data.msg
                loader.hide()
            })  
        },
        priceConverter(price){
            return currencyFormatter.format(price, { code: 'ARS' });
        },
        deleteItem(id){
            this.loading = true

            const token = localStorage.getItem('token_shopuser')
            axios.delete(this.$url+'/cart/delete/'+id, {
                headers: {
                    "Content-Type": 'application/json',
                    "Authorization": `Bearer ${token}`
                }
            }).then((response) => {
                const {data} = response
                this.getCart()
                this.loading = false
                this.$socket.emit('sendCart', true)
            }).catch( error => {
            console.log(error.response.data.msg)
            this.msm_error = error.response.data.msg
            })  
        },
        getAddress(){
            const userId = JSON.parse(localStorage.getItem('data_shopuser'))[1]
            const token = localStorage.getItem('token_shopuser')
            axios.get(this.$url+'/profile/getAddress/'+userId, {
                headers: {
                "Content-Type": 'application/json',
                "Authorization" : `Bearer ${token}`
                }
            }).then((response) => {
                const {data} = response
                this.addresses = data

            }).catch( error => {
                console.log(error.response.data.msg)
            })
        },
        selectDirection(id){
            this.sell.address = id.target.value
        },
        createSale(){
            if(this.sell.address === undefined){
                this.valid = false
                this.msm_error = 'Seleccioná un domicilio de entrega'
                return
            }
            if(this.shipMethodSelected === ''){
                this.valid = false
                this.msm_error = 'Seleccioná un método de envío'
                return
            }
            this.validSale = true
            this.sale.shippingPrice = this.shippingCost
            this.sale.shipMethod = this.shipMethodSelected
            this.sale.saleDetail = this.saleDetail
            this.sale.address = this.sell.address
            
            const token = localStorage.getItem('token_shopuser')
            axios.post(this.$url+'/sales/save', this.sale, {
                headers: {
                    "Content-Type": 'application/json',
                    "Authorization" : `Bearer ${token}`
                }
            }).then((response) => {
                const {data} = response
                this.$socket.emit('sendCart', true)
                this.validSale = true
                console.log(data)
                this.saleID = data._id
                this.mercadoPagoPref()

                /*setTimeout(() => {
                    this.$router.push({name: 'order', params: {id:data._id}})
                }, 2000);*/
            }).catch( error => {
                console.log(error.response.data.msg)
            }) 
        },

        mercadoPagoPref(){
            if(this.shippingCost > 0){
                this.items.push({
                    title: 'Envío',
                    description: 'Costos de envío',
                    quantity: 1,
                    currency_id: 'ARS',
                    unit_price: this.shippingCost,
                })
            }
            const getUser = JSON.parse(localStorage.getItem('data_shopuser'))
            const user = getUser[1]
            this.valid = true
            this.validSale = true
            const data = {
                back_urls: {
                    success: `${this.$frontendURL}/verify/success/`+this.sell.address+'/'+this.shipMethodSelected+'/'+this.shippingCost,
                    pending: `${this.$frontendURL}/verify/pending`,
                    failure: `${this.$frontendURL}/verify/failure`
                },
                items: this.items,
                metadata: { clientID:user, saleID: this.saleID },
                auto_return: 'approved'
            }
			console.log(data);
            console.log(this.$MPKeyAuth)
            axios.post('https://api.mercadopago.com/checkout/preferences', data, {
                headers: {
                    "Content-Type": 'application/json',
                    "Authorization" : `Bearer ${this.$MPKeyAuth}`
                }
            }).then((response) => {
              const {data} = response
              console.log(data);
              /* window.location.href = data.sandbox_init_point+'?ShipM='+this.shipMethodSelected*/
              this.validSale = false
              this.$socket.emit('sendCart', true)
			  window.location.href = data.init_point

            }).catch( error => {
              console.log(error.response.data.msg)
            }) 
        },

        getShippingMethods(){
            let id
            if(this.cart[0]){
                id = this.cart[0].product.seller
            }
            const token = localStorage.getItem('token_shopuser')
            axios.get(this.$url+'/shipping/methods/'+id, {
                headers: {
                    "Content-Type": 'application/json',
                    "Authorization" : `Bearer ${token}`
                }
            }).then((response) => {
                const {data} = response
                this.shipMethods = data
				if(this.total < this.shipMethods.freeShippingAmount){
					return this.freeShipping = false
				}
				if(this.total >= this.shipMethods.freeShippingAmount){
					this.shippingCost = '0'
					return this.freeShipping = true
				} 
            }).catch( error => {
                console.log(error.response.data.msg)
            })
        },
        getUSDSettings(){
            axios.get(`${this.$url}/public/getusdsettings`, {
                headers: {
                    "Content-Type": 'application/json',
                }
            }).then((response) => {
                this.USDData = response.data[0]
                if(this.USDData.enabled === true){
                    this.USDEnabled = true
                }
                if(this.USDData.enabled === false){
                    this.USDEnabled = false
                }
            }).catch( error => {
                console.log(error)
                console.log(error.response.data.msg)
            })
        },
    }
}
</script>