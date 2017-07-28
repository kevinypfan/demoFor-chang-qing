<template>
 <div class="container">
    <div class="addList">
      <h3>新增單筆:</h3>
      <p v-html="status"></p>
      <label for="name">名稱</label>
      <input id="name" v-model="name" @keyup.enter="addList"/>
      <label for="price">單價</label>
      <input id="price" v-model="price" @keyup.enter="addList"/>
      <label for="qty">數量</label>
      <input id="qty" v-model="qty" @keyup.enter="addList"/>
      <button @click="addList">新增</button>
    </div>
    <div class="allList">
      <h3>購物清單:</h3>
      <table>
        <thead>
          <tr>
            <th>名稱</th>
            <th>單價</th>
            <th>數量</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(p,i) in products">
            <td>{{p.name}}</td>
            <td>{{p.price}}</td>
            <td>{{p.qty}}</td>
            <td>
              <button @click="deleteProduct(i)">刪除</button>
            </td>
          </tr>
        </tbody>
      </table>
      <div class="totlePrice">
        <h3>總價: {{totalPrice}}</h3>
      </div>
    </div>
  </div>
</template>
<script>
    export default {
        data(){
           return {
               products:  [{
                    name: "蘋果",
                    price: 30,
                    qty: 3
                  },
                  {
                    name: "水蜜桃",
                    price: 15,
                    qty: 2
                  },
                  {
                    name: "芒果",
                    price: 35,
                    qty: 1
                  }],
                name: "",
                qty: "",
                price: "",
                status: ""
               
                  }
        },
        methods:{
            addList(){
              this.status = "";
              if(this.name == "" || this.qty == "" || this.price ==""){
                this.status = "請不要空白"
              }
              if(isNaN(this.qty) == true){
                this.status += "<span>數量請輸入數字</span>"
              }
              if(isNaN(this.price) == true){
                this.status += "<span>單價請輸入數字</span>"
              }
              if(this.name != "" && this.qty != "" && this.price !="" && isNaN(this.qty) == false && isNaN(this.price) == false  ){
                var addList = {
                name: this.name,
                qty: this.qty,
                price: this.price
              }
              this.products.push(addList);
              }
                this.name = "";
                this.qty = "";
                this.price = "";
            },
            deleteProduct(id){
                this.products.splice(id,1);
                }
            },
            computed:{
                totalPrice(){
                  var total = 0
                  this.products.forEach((p,i)=>{
                    total += p.qty*p.price
                  })
                  return total
                }
        }
    }
</script>   
<style>
.addList span {
  margin-left: 10px;
}
.addList input {
  padding: 5px;
  margin: 10px;
  width: 60px;
}
.addList button {
  background-color: #222;
  border: 1px solid #000;
  padding: 8px 30px;
  margin-left: 10px;
  border-radius: 8px;
  color: #eee;
}

.allList table {
  text-align: center;
}
.allList table button {
  background-color: #222;
  padding: 5px 30px;
  margin-left: -10px;
  border-radius: 8px;
  color: #eee;
}
.allList table thead {
  background-color: #222;
  color: #ddd;
}
.allList table thead th {
  padding: 7px 30px;
}
.allList table tbody td {
  padding: 5px 30px;
  border: 1px solid #000;
}
.allList table tbody td:nth-child(4) {
  border: none;
}

</style>