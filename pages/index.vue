<template>
  <main>
    <section class="self-center flex flex-col flex-1 items-center justify-center">
      <h1 class="title text-center">Harian Bola</h1>
      <span class="subtitle text-center text-lg font-normal">Update score sepak bola, dan informasi jadwal pertandingan liga eropa & Indonesia terlengkap, serta berita terbaru seputar Indonesia Raya.</span>
    </section>

    <section class="mt-8">
      <h3 class="text-primary-600 dark:text-primary-400 max-w-5xl mx-auto">Berita terkini</h3>
      <posts post-type="bola" :amount="6" />
    </section>
    <a href="https://103.3.61.238/" class="w-full mt-2"><img src="/img/ad1.jpg" alt="JUDIBRO"></a>
  </main>
</template>