<template>


    <div class=" grid gap-x-7  grid-cols-3 h-screen">
        <div
            class="border-solid border-2 border-amber-600 drop-shadow-md bg-gradient-to-r from-indigo-200 via-purple-200 to-pink-200 ">

            <form>
                <h1 style="color: red" class="font-bold text-3xl p-6">Add product</h1>
                <table>

                    <tr>
                        <td><label>Product Name :</label></td>
                        <td><input type="text" v-model="product.productname"
                                class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3 m-5"></td>
                    </tr>
                    <tr>
                        <td><label>Price :</label></td>
                        <td><input type="number" v-model="product.prize"
                                class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3 m-5"></td>
                    </tr>
                    <tr>
                        <td><label>Category :</label></td>
                        <select v-model="product.category" @change="onChangeOfCategory($event)">
                            <option value='Cloths'>Cloths</option>
                            <option value="Shoes">Shoes</option>
                            <option value="Guiter">Guiter</option>
                        </select>
                    </tr>
                      <tr>
                        <td><label>Color :</label></td>
                        <select v-model="product.color" @change="onChangeOfCategory($event)">
                            <option value='yellow'>yellow</option>
                            <option value="Pink">Pink</option>
                            <option value="Brown">Brown</option>
                            <option value='Yellow'>Yellow</option>
                            <option value="Black">Black</option>
                            <option value="Pink">Pink</option>
                        </select>
                    </tr>
                    <tr>
                        <td>
                            <button type="button" class="
          border-solid
          rounded
          border-2 border-indigo-600
          p-3
          bg-gradient-to-r
          from-indigo-500
          via-purple-500
          to-pink-500
        " v-on:click="createNewCard()">
                                Submit
                            </button>
                        </td>

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
                            <a class="sm:text-xl sm:p-2 m-4 cursor-pointer text-white hover:bg-blue-300"
                                @click="selectedCategory = 'all'">All</a>
                            <a class="sm:text-xl sm:p-2 m-4 text-white cursor-pointer hover:bg-blue-300"
                                @click="selectedCategory = 'Shoes'">Shoes</a>
                            <a class="sm:text-xl sm:p-2 m-3 text-white cursor-pointer hover:bg-blue-300"
                                @click="selectedCategory = 'Cloths'">Cloths</a>
                            <a class="sm:text-xl sm:p-2 m-4 cursor-pointer text-white hover:bg-blue-300"
                                @click="selectedCategory = 'Guiter'">Guiter</a>
                            <input
                                class="placeholder:italic  bg-white w-50 border border-slate-300 rounded-md m-5 py-2 pl-9 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm"
                                placeholder="Search for Category..." type="text" @input="searchInput($event)"
                                name="search" />

                        </div>

                    </div>
                </nav>

            </div>
            <br>
            <div class="flex">
                {{showAllProducts}}
                <div class="m-10 h-52 w-52 border-4 border-indigo-600" v-for="(prod, prodIndex) in filteredRecords" :key="'id' + prodIndex">
                    <img :src="prod.img" class="h-32 w-52">
                    product Name: <b>{{ prod.productname }}</b>
                    prize: <b>{{ prod.prize }}</b>
                    Category:<b>{{ prod.category }}</b>
                    Color:<b>{{ prod.color }}</b>
                </div>

            </div>

           

        </div>
    </div>

</template>
<script>
export default {
    
    name: 'productForm',
    data() {
        return {
            products: [],
           
            selectedCategory: 'all',
            product: {
                productname: null,
                prize: null,
                category: null,
                img: '',
                color:''
            },
            searchText: '',
        };
    },
    
    computed: {
          showAllProducts() {
        this.products = JSON.parse(sessionStorage.getItem("new"))
        },
        filteredRecords() {
            if (this.searchText) {
                return this.products.filter(user => user.category.toLowerCase().includes(this.searchText.toLowerCase()))
            }
            if (this.selectedCategory !== 'all') {
                return this.products.filter(user => user.category === this.selectedCategory);
 
            }
            return this.products;
        }
    },

    methods: {
       
        createNewCard() {
            if (!isNaN(this.product.productname) || this.product.productname == 'null' || this.product.productname == '') {
                alert("Please Enter Name");

                this.resetForm();
            }
               else if(this.product.prize==""){
                        alert("Please Enter prize");

                        this.resetForm();
                }
            else if (this.product.category == "") {
                alert("Please select category");

                this.resetForm();
            }
            else {
                  this.products.push(this.product);
                // this.products.push(user);

            }
             sessionStorage.setItem("new", JSON.stringify(this.products));

            this.product = {
                productname: '',
                prize: '',
                category: ''
            }
        },
        
        resetForm() {
            this.product = {
                productname: '',
                prize: '',
                category: ''
            }
        },
        onChangeOfCategory(event) {
            console.log(event.target.value);
            if (event.target.value == 'Cloths' && event.target.value=='Red') {
                this.product.img = 'Assetss/cloths.jpg';
            }
            else if (event.target.value == 'Cloths' && event.target.value=='yellow'){
                 this.product.img = 'Assetss/cloth.jpg';
            }
            // else if (event.target.value == 'Shoes'||event.target.value=='Red') {
            //     this.product.img = 'Assetss/shoes.jpg';
            // }
            // else if (event.target.value == 'Guiter'||event.target.value=='Red') {
            //     this.product.img = 'Assetss/guiter.jpg';
            // }
        },
        onChangeOfColor(event){},
        
        searchInput(evt) {
            this.searchText = evt.target.value;
        }


    }
}
</script>