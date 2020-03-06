<template>
  <div>
    <h1> Hello {{ title }}</h1>

  <ul>
    <li v-for="(item, index) in goods" :key="index">
      {{index}}:

      {{item.text}}

      
      |

      {{item.price}}

      <button @click="add(index)">添加购物车</button>
    </li>
  </ul>
  <Cart :data="cart" @addNum="onAdd" @delNum="onDelete"></Cart>
  
  </div>


</template>


<script>
import Cart from "./components/Cart";
export default {
  components: {
    Cart
  },
  data(){
    return {
      title: 'kaikeba',
      goods: [
        {text: 'javaScript全栈', price: '20'},
        {text: 'Html基础', price: '15'},
        {text: 'CSS开发思想', price: '30'},
        {text: '百万年薪架构师', price: '55'},
      ],
      cart: []
    }
  },

  methods: {
    add(i) {
      
      let item = this.goods[i];
      let good = this.cart.find(k=>k.text == item.text);

      if(good){
        good.count += 1;
      }else{
        this.cart.push({...item, count: 1})
      }
    },

    onAdd({arg}) {
      let {index} = arg;

      //这里的index为什么可以直接使用
      this.cart[index].count++;
    },

    onDelete(arg) {
      let {index} = arg;

      if(this.cart[index].count > 1) {
        this.cart[index].count--;
      }else{
        this.cart.splice(index, 1)
      }

      
    },
  }
}
</script>

<style>
  h1 {
    color: red;
  }
</style>