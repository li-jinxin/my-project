<template>
    <div>
        <h2>购物车</h2>

        <table border="1">
            <tr>
                <td>商品</td>
                <td>单价</td>
                <td>价格</td>
                <td>总量</td>
                <td>操作</td>
            </tr>
            <tr v-for="(c, index) in data" :key="index">
                <td>{{c.text}}</td>
                <td>{{c.price}}</td>
                <td>{{c.price * c.count}}</td>
                <td>{{c.count}}</td>
              <td>
                <button @click="delCart(index)">-</button>
                <button @click="addCart(index)">+</button>
              </td>
            </tr>
            <p>总价{{total}}元</p>
          </table>
    </div>
</template>

<script>
export default {
    props: ['data'],
    computed: {
        total() {
            return this.data.reduce((sun, v) => {
                return sun + v.price * v.count;
            }, 0)
        }
    },
    methods: {
        addCart(i) {
            // this.data[i].count += 1;
            this.$emit('addNum', {index: i})
        },

        delCart(i) {
            this.$emit('delNum', {index: i})
        }
    }
}
</script>

<style>

</style>