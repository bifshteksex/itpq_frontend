<script lang="ts">
  import "../app.css";
  import { onMount } from "svelte";
  import Header from "$lib/components/Header.svelte";
  import Footer from "$lib/components/Footer.svelte";

  // Управление состоянием темы
  let darkTheme: boolean;

  onMount(() => {
    const savedTheme = localStorage.getItem("theme");
    if (savedTheme) {
      darkTheme = savedTheme === "dark";
    } else {
      // Проверка предпочтений пользователя
      const prefersDarkScheme = window.matchMedia(
        "(prefers-color-scheme: dark)"
      ).matches;
      darkTheme = prefersDarkScheme;
    }

    // Применение начальной темы
    document.documentElement.classList.toggle("dark", darkTheme);
  });

  function toggleTheme() {
    darkTheme = !darkTheme;
    document.documentElement.classList.toggle("dark", darkTheme);

    // Сохранение выбора пользователя в localStorage
    localStorage.setItem("theme", darkTheme ? "dark" : "light");
  }
</script>

<div class="min-h-screen flex flex-col">
  <Header {toggleTheme} />
  <slot />
  <Footer />
</div>

<style>
  :global(html) {
    @apply bg-white text-gray-900;
  }
  :global(html.dark) {
    @apply bg-gray-900 text-white;
  }
</style>
