<template>
  <div class="goods-items" @click="itemClick">
    <img v-lazy="showImage" alt="" @load="imgLoad" />
    <div class="goods-info">
      <p>{{ goodsItem.title }}</p>
      <span class="price">{{ goodsItem.price }}</span>
      <span class="collect">{{ goodsItem.cfav }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GoodsListItem',
  props: {
    goodsItem: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  computed: {
    showImage () {
      return this.goodsItem.img || this.goodsItem.image || this.goodsItem.show.img
    }
  },
  methods: {
    imgLoad () {
      this.$bus.$emit('itemImageLoad')
    },
    itemClick () {

      this.$router.push('/detail/' + this.goodsItem.iid)
    }
  }
}
</script>

<style scoped>
.goods-items {
  padding-bottom: 40px;
  position: relative;
  /* margin: 0 10px; */
  width: 45%;
}
.goods-items img {
  width: 100%;
  border-radius: 5%;
}

.goods-info {
  font-size: 13px;
  position: absolute;
  bottom: 5px;
  left: 0;
  right: 0;
  overflow: hidden;
  text-align: center;
}

.goods-info p {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-bottom: 3px;
}

.goods-info .price {
  color: var(--color-high-text);
  margin-right: 20px;
}

.goods-info .collect {
  position: relative;
}

.goods-info .collect::before {
  content: '';
  position: absolute;
  left: -15px;
  top: 0;
  width: 14px;
  height: 14px;
  background: url('~assets/img/common/collect.svg') 0 0/14px 14px;
}
</style>
