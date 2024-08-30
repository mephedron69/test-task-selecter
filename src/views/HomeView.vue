<template>
  <div class="basket container">
    <p class="basket-title">Корзина</p>
    <div class="basket__content">
      <div class="basket__content__left">
        <div class="basket__content__left__top">
          <div class="basket__content__left__top-selected" v-if="selectedMultiple.length">
              <div class="basket__content__bot__products" v-for="item in selectedMultiple" :key="item.id">
                <img :src="require(`@/assets/images${item.image}`)"/>
              </div>
          </div>
          <p class="basket__content__left__top-not" v-else>Ничего не выбрано.</p>
        </div>
        <div class="basket__content__bot">
          <div class="basket__content__bot__products" v-for="item in products.slice(0, 8)" :key="item.id" @click="selectProductsMultiple(item)"> 
            <img :src="require(`@/assets/images${item.image}`)"/>
            <div class="basket__content__bot__products-order" v-if="selectedMultiple.includes(item)">
              {{ selectedMultiple.includes(item) ? selectedMultiple.indexOf(item) + 1 : '' }}
            </div>
          </div>
        </div>
      </div>
      <div class="basket__content__right">
        <div class="basket__content__right__top">
          <div class="basket__content__right__top-single" v-if="selectedSingle && Object.keys(selectedSingle).length">
            <img :src="require(`@/assets/images${selectedSingle.image}`)"/>
          </div>
          <p class="basket__content__left__top-not" v-else>Ничего не выбрано.</p>
        </div>
        <div class="basket__content__bot">
          <div class="basket__content__bot__products" v-for="item in products.slice(8, 16)" :key="item.id" @click="selectProductsSingle(item)">
            <img :src="require(`@/assets/images${item.image}`)"/>
            <div class="basket__content__bot__products-delete" v-if="item.id == selectedSingle.id" @click="selectedSingle = {}"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedMultiple: [],
      selectedSingle: {},
      products: [
        { id: 1, name: "Shoes 1", image: '/shoes/s1.png' },
        { id: 2, name: "Shoes 2", image: '/shoes/s2.png' },
        { id: 3, name: "Shoes 3", image: '/shoes/s3.png' },
        { id: 4, name: "Shoes 4", image: '/shoes/s4.png' },
        { id: 5, name: "T-shirt 1", image: '/shirt/t1.png' },
        { id: 6, name: "T-shirt 2", image: '/shirt/t2.png' },
        { id: 7, name: "T-shirt 3", image: '/shirt/t3.png' },
        { id: 8, name: "T-shirt 4", image: '/shirt/t4.png' },
        { id: 11, name: "Jacket 1", image: '/jackets/j1.png' },
        { id: 12, name: "Jacket 2", image: '/jackets/j2.png' },
        { id: 13, name: "Jacket 3", image: '/jackets/j3.png' },
        { id: 14, name: "Jacket 4", image: '/jackets/j4.png' },
        { id: 15, name: "Hoodie 1", image: '/hoodie/h1.png' },
        { id: 16, name: "Hoodie 2", image: '/hoodie/h2.png' },
        { id: 17, name: "Hoodie 3", image: '/hoodie/h3.png' },
        { id: 18, name: "Hoodie 4", image: '/hoodie/h4.png' }
      ]
    }
  },
  methods: {
    selectProductsMultiple(value) {
      const index = this.selectedMultiple.findIndex(item => item.id === value.id);
      if (index !== -1) {
        this.selectedMultiple.splice(index, 1);
      } else {
        this.selectedMultiple.push(value);
      }
    },
    selectProductsSingle(value) {
      this.selectedSingle = value;
    }
  }
}
</script>

<style lang="scss" scoped>
.basket {
  &-title {
    font-size: 24px;
    font-weight: 600;
    margin: 30px 0 20px 0;
  }
  &__content {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    gap: 30px;
    margin-bottom: 50px;
    &__left {
      display: flex;
      flex-direction: column;
      gap: 20px;
      width: 100%;
      &__top {
        width: 50%;
        aspect-ratio: 1;
        background: white;
        border-radius: 5px;
        padding: 15px;
        &-selected {
          display: grid;
          grid-template-columns: repeat(auto-fill, minmax(60px, 1fr));
          gap: 15px;
          row-gap: 15px;
        }
        &-not {
          font-size: 14px;
        }
      }
    }
    &__right {
      display: flex;
      align-items: flex-end;
      flex-direction: column;
      gap: 20px;
      width: 100%;
      &__top {
        width: 50%;
        aspect-ratio: 1;
        background: white;
        border-radius: 5px;
        padding: 15px;
        &-single {
          display: flex;
          align-items: center;
          justify-content: center;
          width: 100%;
          height: 100%;
          img {
            width: 100%;
            height: 100%;
            object-fit: contain;
          }
        }
      }
    }
    
    &__bot {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
      gap: 15px;
      row-gap: 15px;
      background: white;
      padding: 30px 20px 250px 20px;
      border-radius: 5px;
      &__products {
        position: relative;
        cursor: pointer;
        width: 100%;
        aspect-ratio: 1;
        border-radius: 2px;
        overflow: hidden;
        border: 1px solid #d8d8d8;
        background: white;
        img {
          width: 100%;
          height: 100%;
          object-fit: contain;
        }
        &-delete {
          position: absolute;
          top: 0;
          left: 0;
          z-index: 2;
          background: rgba(0, 0, 0, 0.5);
          width: 100%;
          height: 100%;
        }
        &-order {
          position: absolute;
          top: 5px;
          right: 5px;
          width: 20px;
          aspect-ratio: 1;
          border-radius: 50%;
          display: flex;
          align-items: center;
          justify-content: center;
          background: white;
          box-shadow: 0px 4px 14px 0px #00000040;
          font-size: 14px;
        }
      }
    }
  }
}
</style>