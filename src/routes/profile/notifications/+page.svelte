<script lang="ts">
  import { writable } from "svelte/store";

  // User data
  let user = writable({
    firstName: "Иван",
    lastName: "Иванов",
    avatarUrl: "https://placehold.co/150x150",
    birthDate: "1990-01-01",
    email: "ivan.ivanov@example.com",
  });

  // Modal visibility state
  let isSettingsOpen = writable(false);

  function openSettings() {
    isSettingsOpen.set(true);
  }

  function closeSettings() {
    isSettingsOpen.set(false);
  }

  function saveSettings() {
    // Logic to save settings
    closeSettings();
    alert("Настройки сохранены");
  }
</script>

<svelte:head>
  <title>itpq - Личный кабинет</title>
</svelte:head>

<main class="flex-grow py-8 flex flex-col w-full max-w-[1440px] mx-auto">
  <div
    class="w-full flex flex-col md:flex-row justify-between items-start gap-x-10"
  >
    <div class="w-[40%] flex flex-col gap-y-5">
      <div class="flex items-center pb-10 border-b-[1px]">
        <img
          src={$user.avatarUrl}
          alt="Аватар пользователя"
          class="w-24 h-24 rounded-full object-cover mr-4"
        />
        <div>
          <p class="text-2xl font-semibold">
            {$user.firstName}
            {$user.lastName}
          </p>
          <p class="text-sm">Статус поиска работы</p>
          <button
            on:click={openSettings}
            class="mt-2 p-2 bg-gray-300 text-gray-800 rounded-md hover:bg-gray-400"
          >
            <img alt="settings" src="/icons/settings.svg" />
          </button>
        </div>
      </div>

      <ul class="flex flex-col gap-y-3 pb-10 border-b-[1px]">
        <li><a href="/profile">Профиль</a></li>
        <li><a href="/profile/resume/list">Резюме</a></li>
        <li><a href="/profile/responses">Отклики</a></li>
        <li><a href="/profile/favorites">Избранное</a></li>
        <li><a href="/profile/notifications">Настройка уведомлений</a></li>
        <li><a href="/profile/subscriptions">Подписки на компании</a></li>
      </ul>

      <div>
        <button>Выйти</button>
      </div>

      <div
        class="w-full flex items-center justify-center border-[1px] rounded py-3"
      >
        <button>Помощь</button>
      </div>
    </div>

    <div class="w-full">
      <section class="w-full flex flex-col items-center">
        <h2 class="text-2xl font-semibold mb-4">Настройка уведомлений</h2>
      </section>
    </div>
  </div>

  <!-- Modal for user settings -->
  {#if $isSettingsOpen}
    <div
      class="fixed inset-0 bg-gray-900 bg-opacity-80 flex justify-center items-center"
    >
      <div
        class="dark:bg-gray-800 p-6 rounded-md w-full max-w-md relative z-50"
      >
        <h2 class="text-2xl font-bold mb-4">Настройки Личного кабинета</h2>
        <form on:submit|preventDefault={saveSettings}>
          <label class="block mb-2">
            Имя:
            <input
              type="text"
              bind:value={$user.firstName}
              class="border p-2 w-full text-black rounded"
            />
          </label>
          <label class="block mb-2">
            Фамилия:
            <input
              type="text"
              bind:value={$user.lastName}
              class="border p-2 w-full text-black rounded"
            />
          </label>
          <label class="block mb-2">
            Дата рождения:
            <input
              type="date"
              bind:value={$user.birthDate}
              class="border p-2 w-full text-black rounded"
            />
          </label>
          <label class="block mb-2">
            Email:
            <input
              type="email"
              bind:value={$user.email}
              class="border p-2 w-full text-black rounded"
            />
          </label>
          <div class="flex justify-end mt-4">
            <button
              type="button"
              on:click={closeSettings}
              class="mr-2 bg-gray-300 text-gray-800 p-2 rounded-md hover:bg-gray-400"
              >Отмена</button
            >
            <button
              type="submit"
              class="bg-blue-500 text-white p-2 rounded-md hover:bg-blue-600"
              >Сохранить</button
            >
          </div>
        </form>
      </div>
    </div>
  {/if}
</main>
