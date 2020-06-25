<template>
  <div class="v-catalog col-md-10 col-sm-8 col-8 col-lg-12">
    <router-link :to="{name: 'Cart', params: {cart_data: CART}}">
      <div class="cartLink"><i class="fa fa-opencart" aria-hidden="true"></i> {{ CART.length }}</div>
    </router-link>
    <h1>Catalog</h1>
    <div class="v-catalog__list">
      <CatalogItem
      v-for="product in PRODUCTS"
        :key="product.article"
        :product_data="product"
        @AddToCart="AddToCart"
      ></CatalogItem>
    </div>
  </div>
</template>

<script>
import CatalogItem from './v-catalog-item'
import { mapActions, mapGetters } from 'vuex'
export default {
  components: {
    CatalogItem
  },
  data: () => ({
    products: [
      {
        image: 'camp-1.jpg',
        name: 'Rocks',
        price: 7800.0,
        article: 'T1',
        available: true,
        category: 'Oneseason'
      },
      {
        image: 'camp-2.jpg',
        name: 'Greenhouse',
        price: 3150.0,
        article: 'T2',
        available: true,
        category: 'Oneseason'
      },
      {
        image: 'camp-3.jpg',
        name: 'FishingPro',
        price: 4200.0,
        article: 'T3',
        available: false,
        category: 'Allseason'
      },
      {
        image: 'camp-4.jpg',
        name: 'PremierGold',
        price: 10300.0,
        article: 'T4',
        available: true,
        category: 'Allseason'
      },
      {
        image: 'camp-5.jpg',
        name: 'Forest',
        price: 6500.0,
        article: 'T5',
        available: false,
        category: 'Oneseason'
      },
      {
        image: 'camp-6.jpg',
        name: 'Orange',
        price: 3000.0,
        article: 'T6',
        available: true,
        category: 'Oneseason'
      },
      {
        image: 'camp-7.jpg',
        name: 'T-shirt 6',
        price: 8700,
        article: 'T7',
        available: true,
        category: 'Allseason'
      },
      {
        image: 'camp-8.jpg',
        name: 'Hunter',
        price: 7500.0,
        article: 'T8',
        available: true,
        category: 'Allseason'
      },
      {
        image: 'camp-9.jpg',
        name: 'Forest',
        price: 5500.0,
        article: 'T9',
        available: true,
        category: 'Oneseason'
      }
    ]
  }),
  computed: {
    ...mapGetters([
      'PRODUCTS',
      'CART'
    ])
  },
  methods: {
    ...mapActions([
      'GET_PRODUCTS_FROM_API',
      'ADD_TO_CART'
    ]),
    AddToCart (data) {
      this.ADD_TO_CART(data)
    }
  },
  mounted () {
    this.GET_PRODUCTS_FROM_API()
      .then((responce) => {
        if (responce.data) {
          console.log('Data success reload!')
        }
      })
  }
}

</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Kanit&display=swap');
  h1
  {
    font-family: 'Kanit', sans-serif;
  }
.v-catalog{
  margin-left:9%;
}

.v-catalog__list
{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
}
.cartLink
{
  position: absolute;
  top: 0px;
  right: 10px;
  padding: 16px;
  border: solid 3px rgb(18, 104, 29);
  border-radius: 10%;
  background: rgba(241, 241, 241, 0.925);

}
.cartLink:hover
{
background: rgba(81, 187, 95, 0.911) !important;
}
.back
{
  background-color:rgb(17, 95, 23);
  color: #000;
  font-size: 19px;
}
.back:hover
{
  color: #fff;
}
</style>
