<template>
  <div class="grid">
    <div class="grid__wrapper">
      <div class="grid__title">
        Таблица товаров
      </div>
      <div class="grid__form">
        <input type="text" placeholder="Наименование" v-model="name">
        <input type="text" placeholder="Количество" v-model="number">
        <input type="number" placeholder="Цена" v-model="price">
        <button @click.prevent="addProduct">Добавить товар</button>
      </div>
      <table>
        <thead>
          <tr>
            <th>Наименование</th>
            <th>Количество</th>
            <th>Цена</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(product, index) in productInfo">
            <td>
              {{product.name}}
            </td>
            <td>
              {{product.number}}
            </td>
            <td>
              {{product.price}}
            </td>
            <td>
              <button class="btn btn_remove" @click="removeItem(index)">X</button>
              <button class="btn btn_edit" @click="sendItem(index)">Изменить</button>
            </td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <td>Итого:</td>
            <td >
              {{getTotal()}}
            </td>
            <td colspan="2"></td>
          </tr>
        </tfoot>
      </table>
      <div class="grid__form" v-if="change">
        <input type="text" hidden  v-model="editIndex">
        <input type="text"  v-model="editName">
        <input type="text" v-model="editNumber">
        <input type="number"  v-model="editPrice">
        <button @click.prevent="changeProduct">Изменить товар</button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        name: '',
        number: '',
        price: '',
        editName: '',
        editNumber: '',
        editPrice: '',
        editIndex: '',
        change: false,
        productInfo: [
          {
            name: 'Томат',
            number: '12',
            price: '10'
          },
          {
            name: 'Кукуруза',
            number: '32',
            price: '26'
          },
          {
            name: 'Перец',
            number: '22',
            price: '23'
          },
          {
            name: 'Лук',
            number: '14',
            price: '6'
          },
          {
            name: 'Морковь',
            number: '44',
            price: '13'
          }
        ]
      }
    },
    methods: {
      addProduct () {
        this.productInfo.push({
          name: this.name,
          number: this.number,
          price: this.price
        })
        this.name = ''
        this.number = ''
        this.price = ''
      },
      removeItem (i) {
        this.productInfo.splice(i, 1)
      },
      sendItem (i) {
        this.change = true
        this.editName = this.productInfo[i].name
        this.editNumber = this.productInfo[i].number
        this.editPrice = this.productInfo[i].price
        this.editIndex = i
      },
      changeProduct () {
        this.$set(this.productInfo, this.editIndex, {
          name: this.editName,
          number: this.editNumber,
          price: this.editPrice
        })
        this.change = false
      },
      getTotal () {
        return this.productInfo.reduce(function (p, c) {
          return p + c.number * c.price
        }, 0)
      }
    }
  }
</script>

