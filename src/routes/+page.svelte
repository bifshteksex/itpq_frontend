<script lang="ts">
  import { onMount } from "svelte";
</script>

<svelte:head>
  <title>itpq - Recruitment Service</title>
</svelte:head>

<main class="flex-grow py-8 flex flex-col max-w-[1440px] mx-auto">
  <h1 class="text-4xl md:text-5xl font-bold text-center mb-6">
    itpq - поиск вакансий
  </h1>
  <div class="w-full flex flex-col items-center text-center">
    <!-- <input
      type="text"
      placeholder="Поиск вакансий"
      class="w-full p-2 mb-4 border rounded dark:bg-gray-700 dark:text-white"
    /> -->

    <div class="w-full flex flex-col gap-y-5">
      <a
        href="/jobs"
        class="w-full p-2 bg-blue-500 text-white rounded hover:bg-blue-600"
      >
        Список вакансий
      </a>
      <!-- <a
        href="/signup"
        class="w-full p-2 bg-blue-500 text-white rounded hover:bg-blue-600"
      >
        Регистрация
      </a> -->
      <!-- <a
        href="/login"
        class="w-full p-2 bg-blue-500 text-white rounded hover:bg-blue-600"
      >
        Вход
      </a> -->
    </div>
  </div>
</main>
