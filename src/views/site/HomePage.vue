<template>
  <div>
    <SiteBaseNav/>
    <div class="container">
      <div class="text-center" style="
                 background-image: url('https://gamelabiscoitos.com.br/img/brand/bghome.jpg');
                 background-repeat: no-repeat;
                 background-size: cover;
                 background-position: center;
                 min-height: 40vw;
                 ">
			<p class="welcome gamela-color">Gamela, 43 anos de deliciosos momentos</p>
		</div>
    </div>

    <div class="w-100 text-center mt-5">
      <h1 class="font-primary-custom gamela-color gamela-title font-weight-light">Nossa Loja</h1>
    </div>
    <b-carousel
      :interval="5000"
      controls
      indicators
      background="#ababab"
      img-width="1024"
      img-height="480"
    >
      <b-carousel-slide img-src="img/brand/SLIDE/banner_novohorario.png"/>
      <b-carousel-slide img-src="img/brand/SLIDE/banner1.jpg"/>
      <b-carousel-slide img-src="img/brand/SLIDE/banner2.jpg"/>
      <b-carousel-slide img-src="img/brand/SLIDE/banner3.jpg"/>
      <b-carousel-slide img-src="img/brand/SLIDE/banner4.jpg"/>
      <b-carousel-slide img-src="img/brand/SLIDE/banner5.jpg"/>
      <b-carousel-slide img-src="img/brand/SLIDE/frente.jpg"/>
      <b-carousel-slide img-src="img/brand/SLIDE/frente-cor.jpg"/>

    </b-carousel>

    <div class="container">
      <div class="w-100 text-center mt-5">
        <h1 class="font-primary-custom gamela-color gamela-title font-weight-light" style="line-height: 1;">
          Todo momento merece um sabor, principalmente o nosso.
        </h1>
      </div>
      <div class="row">
        <div class="col-md text-center">
          <b-img v-bind="mainProps" thumbnail src="/img/brand/PRODUTOS/paes.jpg"/>
          <router-link class="btn btn-white w-75" :to="{ name: 'produtos' }" disabled="">
            Pães
          </router-link>
        </div>
        <div class="col-md text-center">
          <b-img v-bind="mainProps" thumbnail src="/img/brand/PRODUTOS/biscoitos.jpg"/>
          <router-link class="btn btn-white w-75" :to="{ name: 'produtos' }">
            Biscoitos
          </router-link>
        </div>
        <div class="col-md text-center">
          <b-img v-bind="mainProps" thumbnail src="/img/brand/PRODUTOS/salgados.jpg"/>
          <router-link class="btn btn-white w-75" :to="{ name: 'produtos.categoria', params: { id: 1 } }">
            Salgados
          </router-link>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col-md text-center">
          <b-img v-bind="mainProps" thumbnail src="/img/brand/PRODUTOS/TORDoce.jpg"/>
          <router-link class="btn btn-white w-75" :to="{ name: 'produtos.categoria', params: { id: 3 } }">
            Tortas Doces
          </router-link>
        </div>
        <div class="col-md text-center">
          <b-img v-bind="mainProps" thumbnail src="/img/brand/PRODUTOS/TORSalg.jpg"/>
          <router-link class="btn btn-white w-75" :to="{ name: 'produtos.categoria', params: { id: 2} }">
            Tortas Salgadas
          </router-link>
        </div>
        <div class="col-md text-center">
          <b-img v-bind="mainProps" thumbnail src="/img/brand/PRODUTOS/BoloDoce.jpg"/>
          <router-link class="btn btn-white w-75" :to="{ name: 'produtos.categoria', params: { id: 4 } }">
            Bolos e Doces
          </router-link>
        </div>
      </div>

      <div class="mt-5 text-center">
        <p><a href="./PDF/cardapio_Gamela.pdf" target="_blank">Visualize nosso cardápio em PDF!</a></p>
        <p><a href="./PDF/kit_festa_Gamela.pdf" target="_blank">Veja nosso kit de festas em PDF!</a></p>
      </div>
    </div>
  </div>
</template>

<script>
  import SiteBaseNav from '@/layout/SiteNavbar/SiteBaseNav'
  export default {
    name: 'HomePage',
    components: { SiteBaseNav },
    data() {
      return {
        mainProps: { blank: false, blankColor: '#777', width: 250, height: 250}
      }
    }
  }
</script>

<style lang="scss" scoped>
.welcome{
  padding-top: 150px;
  font-family: Damion-regular;
  letter-spacing: 0;
  font-size: 130px;
  text-transform: inherit;
  position: relative;
  line-height: 0.9em;
  font-weight: bold;
  @media (max-width: 776px) {
    padding-top: 50px;
    padding-bottom: 50px;
    font-size: 95px !important;
  }
}
.gamela-color{
  color: #5E3D0B;
}
.gamela-title{
  font-size: 70px;
}

</style>
