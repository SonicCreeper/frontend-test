<template>
	
	<div class="products_page pg_0">
      <div class="product product_horizontal">                                
          <span class="product_code">Код: {{product["code"]}}</span>
          <div class="product_status_tooltip_container">
              <span class="product_status">Наличие</span>
          </div>                                
          <div class="product_photo">
              <a href="#" class="url--link product__link">
                  <img :src="product['primaryImageUrl']">
              </a>                                    
          </div>
          <div class="product_description">
              <a href="#" class="product__link">{{product['title']}}</a>
          </div>
          <div class="product_tags hidden-sm">
              <p>Могут понадобиться:</p>
              <span v-for='link in assocProducts.split(";\n")'>
                  <a href="#" class="url--link">{{link.slice(0, link.length-1)}}; </a>
              </span>

          </div>
          <div class="product_units">
              <div class="unit--wrapper">
                  <div :class="{'unit--select': true, 'unit--active': isPriceAlt}" @click="isPriceAlt = true" v-if='hasAlt'>
                      <p class="ng-binding">За {{product['unitAlt']}}</p>
                  </div>
                  <div :class="{'unit--select': true, 'unit--active': !isPriceAlt}" @click="isPriceAlt = false">
                      <p class="ng-binding">За {{product['unit']}}</p>
                  </div>
              </div>
          </div>
          <p class="product_price_club_card">
              <span class="product_price_club_card_text">По карте<br>клуба</span>
              <span class="goldPrice">{{priceGold}}</span>
              <span class="rouble__i black__i">
                  <svg version="1.0" id="rouble__b" xmlns="http://www.w3.org/2000/svg" x="0" y="0" width="30px" height="22px" viewBox="0 0 50 50" enable-background="new 0 0 50 50" xml:space="preserve">
                     <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#rouble_black"></use>
                  </svg>
               </span>
          </p>
          <p class="product_price_default">
              <span class="retailPrice">{{priceRetail}}</span>
              <span class="rouble__i black__i">
                  <svg version="1.0" id="rouble__g" xmlns="http://www.w3.org/2000/svg" x="0" y="0" width="30px" height="22px" viewBox="0 0 50 50" enable-background="new 0 0 50 50" xml:space="preserve">
                     <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#rouble_gray"></use>
                  </svg>
               </span>
          </p>
          <div class="product_price_points">
              <p class="ng-binding">Можно купить за 231,75 балла</p>
          </div>
          <div class="list--unit-padd"></div>
          <div class="list--unit-desc">
              <div class="unit--info">
                  <div class="unit--desc-i"></div>
                  <div class="unit--desc-t">
                      <p>
                          <span class="ng-binding">Продается {{unitFull}}<span v-if='hasAlt' style='display: inline;'>:</span></span>
                          <span class="unit--infoInn" v-if='hasAlt'>{{product['unitRatio']}} {{product['unit']}} = {{(+product['unitRatioAlt']).toFixed(3)}} {{product['unitAlt']}} </span>
                      </p>
                  </div>
              </div>
          </div>
          <div class="product__wrapper">
              <div class="product_count_wrapper">
                  <div class="stepper">
                      <input class="product__count stepper-input" type="text" :value="count">
                      <span class="stepper-arrow up" @click='count++'></span>
                      <span class="stepper-arrow down" @click='decCount'></span>                                            
                  </div>
              </div>
              <span class="btn btn_cart" data-url="/cart/" :data-product-id="product['productId']">
                  <svg class="ic ic_cart">
                     <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#cart"></use>
                  </svg>
                  <span class="ng-binding">В корзину</span>
              </span>
          </div>
      </div>
  </div>

</template>

<script>
export default {

  name: 'Item',
  props: ['product'],
  data () {
    return {
    	assocProducts: this.product['assocProducts']+'',
    	isPriceAlt: true,
    	count: 1,
    }
  },
  computed: {
  	priceRetail: function() {
  		const price = +(this.isPriceAlt ? this.product['priceRetailAlt'] : this.product['priceRetail'])
  		return price.toFixed(2)
  	},
  	priceGold: function() {
  		const price = +(this.isPriceAlt ? this.product['priceGoldAlt'] : this.product['priceGold'])
  		return price.toFixed(2)
  	},
  	hasAlt: function() {
  		switch(this.product['unitAlt']) {
  			case this.product['unit']:
  			case '':
  				this.isPriceAlt = false;
  				return false;
  			default:
  				return true;
  		}
  	},
  	unitFull: function() {
  		const unit = this.product['unitFull']
  		switch(unit) {
  			case 'комплект':
  				return unit + 'ами';
  			case 'упаковка':
  			case 'штука':
  				return unit + 'ми';
  			case 'метр погонный':
  				return 'м. погонными';
  		}
  	},
  },
  methods: {
  	decCount: function() {
  		return this.count === 0 ? this.count = 0 : this.count--;
  	}
  }
}
</script>

<style lang="css" scoped>
[v-cloak] {
	visibility: hidden;
}
</style>