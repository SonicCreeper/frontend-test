<template>
  <main class="grid container">
    <div class="sub_category_page">
        <div class="column_right column_right_products_container">
            <div class="product__area" id="app">
                <div id="products_section" v-for="product in products">
                  <Item :product="product"></Item> 
                </div>
            </div>
        </div>
    </div>
  </main>
</template>

<script>
import Item from './Item.vue'
import * as products from '../data/products.json';

export default {
  name: 'app',
  components: {Item},
  data () {
    return {
      products,
    }
  }
}
</script>

<style>
</style>
