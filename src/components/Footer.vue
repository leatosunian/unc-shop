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
                      <li> <router-link to="/products?category=STICKERS#!" class="text-white" href="#">Stickers</router-link></li>
                      <li> <router-link to="/products?category=PARCHES#!" class="text-white" href="#">Parches Textiles</router-link></li>
                    </ul>
                  </div>
                  
                  <div class="mb-3 col-lg-2 col-md-6 mb-lg-0">
                    <h6 class="mb-3 text-white text-uppercase">Clientes</h6>
                    <ul class="list-unstyled">
                      <li> <router-link to="/login" class="text-white">Iniciar Sesión</router-link></li>
                      <li> <router-link to="/login" class="text-white">Quiero registrarme</router-link> </li>
                      <li> <a class="text-white" href="https://api.whatsapp.com/send?phone=5492235892260" target="_blank" >Atención al cliente</a></li>
                    </ul>
                  </div>
                  
                  <div class="col-lg-2">
                    <h6 class="mb-3 text-white text-uppercase">Contactanos</h6>
                    
                    <div style="display:flex; flex-direction:column; gap:8px">
                      <a class="text-muted text-decoration-none" href="#" target="_blank" title="Instagram">
                        <img src="/assets/instagram.png" alt="" style="width:21px; margin-right: 10px;">
                        <span class="text-white">unc7600</span>
                      </a>
                      <a class="text-muted text-decoration-none" href="https://api.whatsapp.com/send?phone=5492235892260" target="_blank" title="Whatsapp">
                        <img src="/assets/whatsapp.png" alt="" style="width:23px; margin-right: 8px;">
                        <span class="text-white">+54 9 223 5 892260</span>
                      </a>
                    </div>

                  </div>

                </div>
              </div>
            </div>
            <!-- Copyright section of the footer-->
            <div class="text-white fw-light" style="background-color: #000000; padding-bottom:1.2rem; padding-top: .4rem;">
              <div class="container">
                <div class="row align-items-center">
                  <div class="text-center col-md-6 text-md-start">
                    <p class="mb-md-0">Unique Nifty Crafts &copy; Todos los derechos reservados. Tienda desarrollada por <a style="color:rgb(254, 75, 0)" target='_blank' href="https://tosunian.dev">tosunian.dev</a> </p>
                  </div>
                  <div class="col-md-6">
                    <ul class="mt-2 mb-0 text-center list-inline mt-md-0 text-md-end">
                      <li class="list-inline-item"><img class="w-2rem" src="https://d19m59y37dris4.cloudfront.net/sell/2-0/img/visa.svg" alt="..."></li>
                      <li class="list-inline-item"><img class="w-2rem" src="https://d19m59y37dris4.cloudfront.net/sell/2-0/img/mastercard.svg" alt="..."></li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
        </footer>
    </div>
</template>

<script>

export default {
  name: 'Footer',
}
</script>
  
  