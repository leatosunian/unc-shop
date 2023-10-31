<template>
    <div>
        <footer class="main-footer">
            
            <!-- Main block - menus, subscribe form-->
            <div class="text-muted borde" style="background-color: #000000; padding-top: 2.4rem;"> 
              <div class="container">
                <div class="row">

                  <div class="mb-5 col-lg-4 mb-lg-0">
                    <div class="mb-3 text-lg fw-bold text-uppercase text-dark">
                      <img src="@/assets/footerlogo.png" style="width:240px;" alt="eMart brand logo">
                      <!-- <img src="@/assets/new-deco.png" class="logoImg" style="width:47px!important;" alt=""> -->
                    </div>
                    
                  </div>
                  
                  <div class="mb-3 col-lg-2 col-md-6 mb-lg-0">
                    <h6 class="mb-3 text-white text-uppercase">Shop</h6>
                    <ul class="list-unstyled">
                      <li> <router-link to="/products?category=STICKERS#!" class="text-white orangeHover" href="#">Stickers</router-link></li>
                      <li> <router-link to="/products?category=PARCHES#!" class="text-white orangeHover" href="#">Parches Textiles</router-link></li>
                    </ul>
                  </div>
                  
                  <div class="mb-3 col-lg-2 col-md-6 mb-lg-0">
                    <h6 class="mb-3 text-white text-uppercase">Clientes</h6>
                    <ul class="list-unstyled">
                      <li> <router-link to="/login" class="text-white orangeHover">Iniciar Sesión</router-link></li>
                      <li> <router-link to="/login" class="text-white orangeHover">Quiero registrarme</router-link> </li>
                      <li><span v-b-modal.modal-lg-buy variant="primary" class="orangeHover" style="border:none; margin-top:0px; margin-left:0!important;" >
                        Cómo comprar
                      </span></li>
                      <li> <a class="text-white orangeHover" href="https://api.whatsapp.com/send?phone=5492235892260" target="_blank" >Atención al cliente</a></li>
                    </ul>


                  <b-modal id="modal-lg-buy" size="lg" title="Cómo comprar" >
                    <div style="display:flex;flex-direction:column;padding:0 30px; gap:10px">
                      <span style="font-weight:600; font-size: 18px;">
                          - Registrate e iniciá sesión
                          <p style="font-weight:400; font-size: 17px;">Para comprar debes ser un usuario registrado. Creá tu cuenta haciendo <router-link to="/login">click acá</router-link> y luego iniciá sesión.</p>
                      </span>
                      <span style="font-weight:600; font-size: 18px;">
                          - Agregá un domicilio de entrega
                          <p style="font-weight:400; font-size: 17px;">En las configuraciones de tu cuenta, ingresá hasta dos direcciones de envío para seleccionar al hacer tus compras.</p>
                      </span>
                      <span style="font-weight:600; font-size: 18px; margin-bottom: 16px;">
                        - Agregá productos a tu carrito
                      </span>
                      <span style="font-weight:600; font-size: 18px;">
                        - Realizá el pedido
                        <p style="font-weight:400; font-size: 17px;">Elegí cómo querés que te llegue tu pedido, seleccioná tu dirección de envío que agregaste anteriormente y aboná tu compra de manera segura mediante MercadoPago.</p>
                      </span>
                      <span style="font-weight:600; font-size: 18px;">
                        - Cómo sigo mi pedido?
                        <p style="font-weight:400; font-size: 17px;">Cuando despachemos tu pedido, te enviaremos un código de seguimiento para que sigas el estado de tu compra. Éste lo podrás ver ingresando a Mis pedidos, donde en el detalle del pedido se mostrará luego de que te lo enviemos. </p>
                      </span>
                    </div>
                    <template #modal-footer>
                      <div class="">
                        
     
                      </div>
                    </template>
                  </b-modal>
                  </div>
                  
                  <div class="col-lg-2">
                    <h6 class="mb-3 text-white text-uppercase">Contactanos</h6>
                    
                    <div style="display:flex; flex-direction:column; gap:8px">
                      <a class="text-muted text-decoration-none" href="#" target="_blank" title="Instagram">
                        <img src="/assets/instagram.png" alt="" style="width:21px; margin-right: 10px;">
                        <span class="text-white orangeHover">unc7600</span>
                      </a>
                      <a class="text-muted text-decoration-none" href="https://api.whatsapp.com/send?phone=5492235892260" target="_blank" title="Whatsapp">
                        <img src="/assets/whatsapp.png" alt="" style="width:23px; margin-right: 8px;">
                        <span class="text-white orangeHover">+54 9 223 5 892260</span>
                      </a>
                    </div>

                  </div>

                </div>
              </div>
            </div>
            <!-- Copyright section of the footer-->
            <div class="text-white fw-light" style="background-color: #000000; padding-bottom:1.2rem; padding-top: 2rem;">
              <div class="container">
                <div class="row align-items-center">
                  <div class="text-center col-md-6 text-md-start">
                    <p class="mb-md-0">Unique Nifty Crafts &copy; Todos los derechos reservados. Tienda desarrollada por <a style="color:rgb(254, 75, 0)" target='_blank' href="https://tosunian.dev">tosunian.dev</a> </p>
                  </div>
                  <div class="col-md-6">
                    <ul class="mt-2 mb-0 text-center list-inline mt-md-0 text-md-end">
                      <li class="list-inline-item">
                        <img class="w-2rem" src="https://d19m59y37dris4.cloudfront.net/sell/2-0/img/visa.svg" alt="...">
                      </li>
                      <li class="list-inline-item">
                        <img class="w-2rem" src="https://d19m59y37dris4.cloudfront.net/sell/2-0/img/mastercard.svg" alt="...">
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
        </footer>
    </div>
</template>

<style>
  .orangeHover {
    color: white;
    transition: .3s all ease-in-out;
  }
  .orangeHover:hover {
    color: rgb(254, 75, 0) !important;
    transition: .3s all ease-in-out;
    text-decoration: none;
  }
</style>

<script>

export default {
  name: 'Footer',
}
</script>
  
  