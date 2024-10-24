<script lang="ts">
  // Здесь можно добавить любую логику или функции, связанные с авторизацией
  let email = "";
  let password = "";

  function handleLogin() {
    // Логика обработки авторизации пользователя
    console.log(`Logging in user: ${email}`);
  }
</script>

<svelte:head>
  <title>itpq - Вход в систему</title>
</svelte:head>

<main class="flex-grow flex flex-col">
  <div class="flex">
    <div class="w-[70%] h-[calc(100vh-144px)]">
      <video class="w-full h-full object-cover" width="320" height="240" autoplay muted loop>
        <source src="/video/login.mp4" type="video/mp4" />
        Your browser does not support the video tag.
      </video>
    </div>
    <div class="w-full flex flex-col items-center justify-center px-5">
      <div class="w-full max-w-lg flex flex-col gap-y-5">
        <button class="p-2 bg-red-500 text-white rounded hover:bg-blue-600"
          >Войти с помощью Google</button
        >
        <button class="p-2 bg-white text-black rounded hover:bg-blue-600"
          >Войти с помощью Apple</button
        >
        <button class="p-2 bg-blue-500 text-white rounded hover:bg-blue-600"
          >Войти с помощью VK ID</button
        >
        <button class="p-2 bg-blue-500 text-white rounded hover:bg-blue-600"
          >Войти с помощью Telegram</button
        >
      </div>

      <p class="text-xs my-5">или</p>

      <form
        on:submit|preventDefault={handleLogin}
        class="w-full max-w-lg flex flex-col items-center"
      >
        <input
          type="email"
          placeholder="Электронная почта"
          bind:value={email}
          class="w-full p-2 mb-4 border rounded dark:bg-gray-700 dark:text-white"
          required
        />
        <!-- <input
        type="password"
        placeholder="Пароль"
        bind:value={password}
        class="w-full p-2 mb-4 border rounded dark:bg-gray-700 dark:text-white"
        required
      /> -->
        <button
          type="submit"
          class="w-full p-2 bg-blue-500 text-white rounded hover:bg-blue-600"
        >
          Войти
        </button>
      </form>
      <p class="text-xs mt-1">
        Не помните данные для входа? <a class="underline" href="/"
          >Кликните сюда</a
        >
      </p>
    </div>
  </div>
</main>
