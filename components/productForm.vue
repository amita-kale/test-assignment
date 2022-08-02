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
                    <select v-model="product.category" @change="onChangeOfCategory($event)">
                        <option value='Cloths'>Cloths</option>
                         <option value="Shoes">Shoes</option>
                          <option value="Guitar">Guitar</option>
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
        <div class="bg-indigo">
            
            <nav
        class="sm:relative w-full sm:flex  sm:  items-center sm:justify-between py-2  bg-purple-300 text-black-500 hover:text-gray-700 focus:text-gray-700 shadow-lg">
        <div class="sm:container-fluid w-full sm:flex  items-center justify-between px-2">
        <div class="sm:container-fluid">
        <a class="sm:text-xl sm:p-2 m-3 text-white hover:bg-blue-300" @click="searchOnlyCloth">Cloths</a>
        <a class="sm:text-xl sm:p-2 m-4 text-white hover:bg-blue-300" @click="searchOnlyShoes" >Shoes</a>
        <a class="sm:text-xl sm:p-2 m-4 text-white hover:bg-red-300" @click="searchOnlyGuitar">Guitar</a>  
        <input class="placeholder:italic  bg-white w-50 border border-slate-300 rounded-md m-5 py-2 pl-9 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm" placeholder="Search for Category..." type="text" @input="searchInput($event)"  name="search"/>

      </div>
     
    </div>
  </nav>
            
            </div>
       <br>
      <div class="flex">
       
        <div class="m-10 h-52 w-52 border-4 border-indigo-600" v-for="(prod) in filteredRecords" :key="prod">
        <img :src="prod.img" class="h-32 w-52"> 
           product Name: <b>{{prod.productname}}</b>
           prize:  <b>{{prod.prize}}</b>
           Category:<b>{{prod.category}}</b>
        </div>
        
    </div>

     <div v-if="this.shoes==true" class="flex">
       
        <div class="m-10 h-52 w-52 border-4 border-indigo-600" v-for="item in this.shoesArr" :key="item">
        <!-- <span v-if="item.category =='Shoes'"> -->
            <img :src="item.img" class="h-32 w-52"> 
            product Name: <b>{{item.productname}}</b>
            prize:  <b>{{item.prize}}</b>
            Category:<b>{{item.category}}</b>
        <!-- </span> -->
        </div>
        
    </div>
    <div v-else-if="this.cloth==true" class="flex">
       
        <div class="m-10 h-52 w-52 border-4 border-indigo-600" v-for="item in this.shoesArr" :key="item">
        <!-- <span v-if="item.category =='Shoes'"> -->
            <img :src="item.img" class="h-32 w-52"> 
            product Name: <b>{{item.productname}}</b>
            prize:  <b>{{item.prize}}</b>
            Category:<b>{{item.category}}</b>
        <!-- </span> -->
        </div>
        
    </div>

     <div v-else-if="this.guitar==true" class="flex">
       
        <div class="m-10 h-52 w-52 border-4 border-indigo-600" v-for="item in this.shoesArr" :key="item">
        <!-- <span v-if="item.category =='Shoes'"> -->
            <img :src="item.img" class="h-32 w-52"> 
            product Name: <b>{{item.productname}}</b>
            prize:  <b>{{item.prize}}</b>
            Category:<b>{{item.category}}</b>
        <!-- </span> -->
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
    cloth:false,
    shoes:false,
    guitar:false,
    shoesArr : [],    
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
      if(event.target.value=='Cloths'){
        this.product.img='Assetss/cloths.jpg';
      }
      else if(event.target.value=='Shoes'){
        this.product.img='Assetss/shoes.jpg';
      }
       else if(event.target.value=='Guiter'){
        this.product.img='Assetss/guiter.jpg';
      }
    },
     searchOnlyCloth(){
      
        this.cloth=true;
        this.shoesArr = this.products.filter(e => {
            if(e.category=='Cloths'){
                return e;
            }
        })
    },
    searchOnlyGuitar(){
      
        this.guitar=true;
        this.shoesArr = this.products.filter(e => {
            if(e.category=='Guitar'){
                return e;
            }
        })
    },
    searchOnlyShoes(){
      
        this.shoes=true;
        this.shoesArr = this.products.filter(e => {
            if(e.category=='Shoes'){
                return e;
            }
        })
    },
     searchInput(evt){
      this.searchText = evt.target.value;
       
    },


  }

}
</script>