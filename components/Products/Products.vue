<template>
<view style="display: flex;">
  <view class="products_css">
    <view class="products_dw">
      
      
      <view class="products_items">
        <!-- 外层容器控制每行显示2组 -->
        <view class="product_row" v-for="(row, rowIndex) in chunkedGroups" :key="rowIndex">
          <!-- 每组显示2个商品 -->
          <view class="product_group" v-for="(group, groupIndex) in row" :key="groupIndex">
            <view class="product_item" v-for="(item, index) in group" :key="index">
              <img class="products_img" :src="`/static/img/productsimg/${item.img}`" />
              <text class="products_text2">￥{{ item.price }}补贴价</text>
            </view>
          </view>
        </view>
      </view>
      
    </view>
  </view>
</view>
</template>

<script setup>
import {ref, computed} from 'vue';  

const img_name = ref(['2e1b8fb8799f7811.png','2f5e1ba16b33756d.png','9e595b4718645864.png',
'26aa41cfa6b0861b.png','53e707bcd72ba87c.png','84c1891bc49710c1.png',
'757f1139a1ab311a.png','a2c75cc3518c0267.png','00e5b6c483e5f35b.png','4bbbdd3ad34311ca.png','9d946b203fad301e.png','c1df062cc995b006.png'])

const product_price = ref(['516','215','485','100','33','151','156','588','12','42','444','22'])

// 原始分组：每组2个商品
const groupedProducts = computed(() => {
  const groups = [];
  for (let i = 0; i < img_name.value.length; i += 2) {
    groups.push([
      { img: img_name.value[i], price: product_price.value[i] },
      { img: img_name.value[i+1], price: product_price.value[i+1] }
    ].filter(item => item.img));
  }
  return groups;
});

// 将分组后的数据按每2组一行进行分块
const chunkedGroups = computed(() => {
  const result = [];
  for (let i = 0; i < groupedProducts.value.length; i += 2) {
    result.push(groupedProducts.value.slice(i, i + 2));
  }
  return result;
});
</script>

<style lang="scss" scoped>
.products_css {
  width: 100%;
  height: auto;
  background-color: white;
  display: flex;
  border-radius: 20rpx;
  .products_dw {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    background-color: white;
    width: 100%;
    height: auto;
    margin: 20rpx;
    border-radius: 20rpx;
    .products_text1 {
      font-size: 12px;
      font-weight: bold;
      margin-top: 0;
      margin-bottom: 10rpx;
    }
    .products_items {
      width: 100%;
      .product_row {
        display: flex;
        justify-content: space-between;
        margin-bottom: 10rpx;
        .product_group {
          width: 49%; /* 每组占49%宽度 */
          display: flex;
          flex-direction: row;
          border: 2rpx solid #f0f0f0;
          border-radius: 10rpx;
          padding: 10rpx;
          box-sizing: border-box;
          .product_item {
            width: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 5rpx;
            &:last-child {
              margin-bottom: 0;
            }
            .products_img {
              width: 100%;
              height: 148rpx;
              object-fit: contain;
            }
            .products_text2 {
              font-size: 12px;
              font-weight: bold;
              color: red;
              text-align: center;
              margin-top: 5rpx;
            }
          }
        }
      }
    }
  }
}
</style>