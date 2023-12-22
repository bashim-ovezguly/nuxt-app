<template>
  <div class="shadow-md">
    <div class="header flex p-[10px]">
      <a href="/" class="flex">
        <img class="h-full" src="../static/logo_white.png" />
        <div class="text grid">
          <label>Söwda toplumy - MarketPlace</label>
        </div>        
      </a>
      <Camera></Camera>
    </div>
    <div class="flex flex-wrap justify-center sticky top-[0px]">
      <a
        class="p-[10px] hover:text-sky-500 transition-all hover:bg-slate-100"
        href="/"
        >Baş sahypa</a
      >
      <a
        class="p-[10px] hover:text-sky-500 transition-all hover:bg-slate-100"
        href="/stores"
        >Dükanlar</a
      >
      <a class="p-[10px] hover:text-sky-500 transition-all hover:bg-slate-100"
        >Harytlar</a
      >
      <a class="p-[10px] hover:text-sky-500 transition-all hover:bg-slate-100"
        >Bildirişler</a
      >
      <a class="p-[10px] hover:text-sky-500 transition-all hover:bg-slate-100"
        >Awtoulaglar</a
      >

      <Camera></Camera>
    </div>
  </div>
</template>


<script>
  import { Camera } from 'lucide-vue';
  export default {
    name:"HomeHeader",

    components: { Camera }
  };
</script>



<style>
.header {
  height: 90px;
  overflow: hidden;
  background: rgb(10, 35, 98);
}

.header .text label {
  font-weight: bold;
  vertical-align: middle;
  font-size: 30px;
  color: white;
}

.header .text {
  padding: 5px;
  align-items: center;
}
</style>
