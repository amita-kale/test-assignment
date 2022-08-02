<template>


<div class=" grid gap-x-7  grid-cols-3 h-screen" >
    <div class="border-solid border-2 border-amber-600 drop-shadow-md bg-gradient-to-r from-indigo-200 via-purple-200 to-pink-200 ">

        <form>
             <h1 style="color: red" class="font-bold text-3xl p-6">Add product</h1>
            <table>
                
                <tr>
                    <td><label>Product Name :</label></td>
                    <td><input type="text" v-model="product.productname" class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3 m-5"></td>
                </tr>
                 <tr>
                    <td><label>Price :</label></td>
                    <td><input type="number" v-model="product.prize" class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3 m-5"></td>
                </tr>
                 <tr>
                    <td><label>Category :</label></td>
                    <!-- <td><input type="text" v-model="product.category" class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3 m-5"></td> -->
                    <select v-model="product.category" @change="onChangeOfCategory($event)">
                        <option value='cloths'>Cloths</option>
                         <option value="">Shoes</option>
                          <option value="">Other</option>
                    </select>
                </tr>
                <tr>
                    <td>
                    <button
        type="button"
        
        class="
          border-solid
          rounded
          border-2 border-indigo-600
          p-3
          bg-gradient-to-r
          from-indigo-500
          via-purple-500
          to-pink-500
        "
       v-on:click="createNewCard()"
      >
        Submit
      </button></td>
      
                </tr>
            </table>
        </form>

    </div>
    <div class="bg-gray-300 col-span-2">
       <div> <input class="placeholder:italic placeholder:text-slate-400 block bg-white w-50 border border-slate-300 rounded-md m-5 py-2 pl-9 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm" placeholder="Search for Category..." type="text" @input="searchInput($event)"  name="search"/></div><br>
       <br>
      <div class="flex">
        <div class="m-10 h-52 w-52 border-4 border-indigo-600">
        <img src="Assetss/cloths.jpg" class="h-32 w-52">
           product Name: <b>{{"Cloths"}}</b>
           prize:  <b>{{"1000"}}</b>
            Category:<b>{{"Cloths"}}</b>
        </div>
         <div class="m-10 h-52 w-52 border-4 border-indigo-600">
        <img src="Assetss/shoes.jpg" class="h-32 w-52">
           product Name: <b>{{"Shoes"}}</b>
           prize:  <b>{{"1000"}}</b>
           Category:<b>{{"Shoes"}}</b>
        </div>
        <div class="m-10 h-52 w-52 border-4 border-indigo-600" v-for="(prod) in filteredRecords" :key="prod">
        <img :src="prod.img" class="h-32 w-52">
         <!-- <img src="Assetss/guiter.jpg" class="h-45 w-45"> -->
        
           product Name: <b>{{prod.productname}}</b>
           prize:  <b>{{prod.prize}}</b>
           Category:<b>{{prod.category}}</b>
        </div>
        

        
    </div>
    </div>
</div>

</template>
<script>
export default {
   name:'productForm',
   data() {
    return {
    products: [],
      product: {
        productname: null,
        prize: null,
        category:null,
        img:''
      },
       searchText: '',
    };
  },
   computed: {
    filteredRecords() {
      if (this.searchText) {
        return this.products.filter(user => user.category.toLowerCase().includes(this.searchText.toLowerCase()))
      }
      return this.products;
    }
  },
  methods: {
    createNewCard(){
         this.products.push(this.product);
           this.product= {
            productname: '',
            prize: '',
            category:''
      }
    },
    onChangeOfCategory(event) {
      console.log(event.target.value);
      if(event.target.value=='cloths'){
        this.product.img='Assetss/cloths.jpg';
      }
    //   else if()
    },
     searchInput(evt){
      // console.log(evt.target.value);
      this.searchText = evt.target.value;
    },


  }

}
</script>