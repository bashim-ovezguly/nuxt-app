<template>
  <div class="shadow-md">
    <div class="header flex p-[10px] justify-between">
      <a href="/" class="flex">
        <img class="logo h-full" src="../static/logo_white.png" />
        <div class="text grid">
          <label class="project-name">Söwda toplumy - MarketPlace</label>
        </div>
      </a>
      <div class="btns flex items-center">
        <a href="/login" class="hover:text-sky-500">
          <IconUser
            class="text-white w-[40px] h-[40px] transition-all hover:text-sky-500"
          ></IconUser>
        </a>
      </div>
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
      <a
        class="p-[10px] hover:text-sky-500 transition-all hover:bg-slate-100"
        href="/products"
        >Harytlar</a
      >
 
      <a href="/cars" class="p-[10px] hover:text-sky-500 transition-all hover:bg-slate-100"
        >Awtoulaglar</a
      >
    </div>
  </div>
</template>

<script>
import IconUser from '../components/icons/IconUser'
export default {
  name: 'HomeHeader',
  components: { IconUser },
}
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

@media screen and (max-width: 610px) {
  .header .text label {
    font-size: 20px;
  }
}
</style>
