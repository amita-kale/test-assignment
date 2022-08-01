<template>
<div class=" grid gap-x-7  grid-cols-3 h-screen" >
    <div class="border-solid border-2 border-amber-600 drop-shadow-md bg-gradient-to-r from-indigo-200 via-purple-200 to-pink-200 ">

        <form>
            <table>
                <tr>
                    <td><label>Product Name :</label></td>
                    <td><input type="text" class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3 m-5"></td>
                </tr>
                 <tr>
                    <td><label>Price :</label></td>
                    <td><input type="text" class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3 m-5"></td>
                </tr>
                 <tr>
                    <td><label>Category :</label></td>
                    <td><input type="text" class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3 m-5"></td>
                </tr>
                <tr>
                    <td>
                    <button
        type="submit"
        
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
       
      >
        Submit
      </button></td>
                </tr>
            </table>
        </form>

    </div>
    <div class="bg-gray-300 col-span-2">hello</div>
</div>
</template>