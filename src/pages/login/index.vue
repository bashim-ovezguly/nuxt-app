<template>
  <div class="bgk">
    <div class="fields grid w-400px h-max shadow-md rounded-[10px] p-[20px]">
      <label class="text-[30px] text-sky-400 text-bold my-[10px]">Giriş</label>
      <label class="text-[12px] mt-[5px]">Ulanyjy adyňyz</label>
      <input class="border rounded" />
      <label class="text-[12px] mt-[5px]">Açar sözüňiz</label>
      <input class="border rounded" />
      <button
        class="rounded bg-sky-400 text-white p-[2px] my-[5px] text-[14px]"
      >
        Içeri girmek
      </button>
      <button
        class="rounded bg-sky-400 text-white p-[2px] my-[5px] text-[14px]"
      >
        Registrasiýa
      </button>
    </div>
  </div>
</template>

<style>
.bgk {
  display: flex;
  justify-content: center;
}

.fields {
  background: white;
  min-width: 300px;
  margin-top: 5%;
}
</style>
