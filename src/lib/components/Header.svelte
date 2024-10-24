<script lang="ts">
  import { onMount } from "svelte"; // Импортируем onMount для работы с событиями
  export let toggleTheme: () => void;
  let showDropdown = false; // Состояние для управления видимостью дропдауна
  let dropdownRef: HTMLElement | null = null; // Ссылка на элемент дропдауна

  // Функция для переключения состояния дропдауна
  function toggleDropdown() {
    showDropdown = !showDropdown;
  }

  // Обработчик кликов вне дропдауна
  function handleClickOutside(event: MouseEvent) {
    if (dropdownRef && !dropdownRef.contains(event.target as Node)) {
      showDropdown = false;
    }
  }

  // Добавляем обработчик при монтировании компонента
  onMount(() => {
    document.addEventListener("click", handleClickOutside);

    // Очищаем обработчик при размонтировании компонента
    return () => {
      document.removeEventListener("click", handleClickOutside);
    };
  });
</script>

<header
  class="p-4 bg-gray-100 dark:bg-gray-800"
>
  <div class="flex justify-between items-center max-w-[1440px] mx-auto">
    <a href="/"><h1 class="text-xl font-bold">itpq 🐐</h1></a>
    <nav class="flex items-center gap-x-8 relative">
      <a href="/jobs" class="hover:underline">Вакансии</a>
      <a href="/login" class="hover:underline">Вход</a>

      <!-- Личный кабинет с дропдауном -->
      <div class="relative" bind:this={dropdownRef}>
        <button on:click={toggleDropdown} class="hover:underline">
          Личный кабинет
        </button>
        {#if showDropdown}
          <div
            class="absolute right-0 mt-2 w-48 bg-white dark:bg-gray-700 rounded-md shadow-lg z-10"
          >
            <a
              on:click={toggleDropdown}
              href="/profile"
              class="block px-4 py-2 text-gray-800 dark:text-white hover:bg-gray-100 dark:hover:bg-gray-600"
            >
              Профиль
            </a>
            <!-- <a
              on:click={toggleDropdown}
              href="/"
              class="block px-4 py-2 text-gray-800 dark:text-white hover:bg-gray-100 dark:hover:bg-gray-600"
            >
              Настройки
            </a> -->
          </div>
        {/if}
      </div>
    </nav>

    <button
      on:click={toggleTheme}
      class="p-2 rounded bg-gray-200 dark:bg-gray-700 text-gray-800 dark:text-white"
    >
      <span class="hidden md:block">Переключить тему</span>
      <span class="md:hidden">x</span>
    </button>
  </div>
</header>
