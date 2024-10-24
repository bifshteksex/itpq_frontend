<script lang="ts">
  let name = "";
  let surname = "";
  let email = "";
  let password = "";
  let repeatPassword = "";

  function handleSignup() {}
</script>

<svelte:head>
  <title>itpq - Регистрация</title>
</svelte:head>

<main class="flex-grow p-8 flex flex-col items-center">
  <h1 class="text-4xl md:text-5xl font-bold text-center mb-6">Регистрация</h1>
  <form
    on:submit|preventDefault={handleSignup}
    class="w-full max-w-lg flex flex-col items-center"
  >
    <input
      type="text"
      placeholder="Имя"
      bind:value={name}
      class="w-full p-2 mb-4 border rounded-md dark:bg-gray-700 dark:text-white"
      required
    />
    <input
      type="text"
      placeholder="Фамилия"
      bind:value={surname}
      class="w-full p-2 mb-4 border rounded-md dark:bg-gray-700 dark:text-white"
      required
    />
    <input
      type="email"
      placeholder="Электронная почта"
      bind:value={email}
      class="w-full p-2 mb-4 border rounded-md dark:bg-gray-700 dark:text-white"
      required
    />
    <input
      type="password"
      placeholder="Пароль"
      bind:value={password}
      class="w-full p-2 mb-4 border rounded-md dark:bg-gray-700 dark:text-white"
      required
    />
    <input
      type="password"
      placeholder="Повторите пароль"
      bind:value={repeatPassword}
      class="w-full p-2 mb-4 border rounded-md dark:bg-gray-700 dark:text-white"
      required
    />
    <button
      type="submit"
      class="w-full p-2 bg-blue-500 text-white rounded-md hover:bg-blue-600"
    >
      Зарегистрироваться
    </button>
  </form>
</main>
