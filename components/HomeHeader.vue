<template>
  <div class="header flex shadow-md sticky top-[0px]">
    <a href="/" class="flex">
      <img class="h-full" src="../static/logo_white.png">
      <div class="text grid">
        <label>Söwda toplumy - MarketPlace</label>
      </div>
    </a>
   
  </div>
</template>

<style>
  .header{
    box-shadow: 1px 1px 5px gainsboro;
    height: 90px;
    overflow: hidden;
    padding: 10px;
    background: rgb(10, 35, 98);
  }

  .header .text label{
    font-weight: bold;
    vertical-align: middle;
    font-size: 30px;
    color: white;
  }

  .header .text{
    padding: 5px;
    align-items: center;
  }

</style>
