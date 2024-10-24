<script lang="ts">
  import { writable } from "svelte/store";

  interface Job {
    id: number;
    title: string;
    company: string;
    location: string;
    description: string;
    payment: string;
  }

  let jobs: Job[] = [
    {
      id: 1,
      title: "Frontend Developer",
      company: "Company A",
      location: "Moscow",
      description: "Job description A",
      payment: "100₽",
    },
    {
      id: 2,
      title: "Backend Developer",
      company: "Company B",
      location: "Saint Petersburg",
      description:
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed congue ante sed vehicula auctor. Maecenas scelerisque ante id lectus blandit, pulvinar laoreet ante fermentum. Suspendisse sed volutpat ligula, non volutpat nisl. Duis dui ipsum, cursus in finibus id, gravida et eros. Phasellus commodo nulla at lectus dictum, ac ullamcorper diam ultricies. Aliquam laoreet semper justo, eu hendrerit sapien aliquam in. Cras neque est, ullamcorper et tortor eget, aliquet molestie purus. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. In sit amet purus tristique, rhoncus ligula quis, elementum risus. Mauris aliquam nunc molestie nunc venenatis, in facilisis mauris scelerisque. Donec semper ultrices nulla, eu consequat ante condimentum non. Proin non nisl nisl.",
      payment: "1000000₽",
    },
    {
      id: 3,
      title: "Backend Developer",
      company: "Company C",
      location: "Saint Petersburg",
      description: "Job description C",
      payment: "1000₽",
    },
    {
      id: 4,
      title: "Backend Developer",
      company: "Company D",
      location: "Saint Petersburg",
      description: "Job description D",
      payment: "100₽",
    },
    {
      id: 5,
      title: "Backend Developer",
      company: "Company E",
      location: "Saint Petersburg",
      description: "Job description E",
      payment: "100₽",
    },
    {
      id: 6,
      title: "Backend Developer",
      company: "Company F",
      location: "Saint Petersburg",
      description: "Job description F",
      payment: "100₽",
    },
  ];

  let currentPage: number = 1;
  let itemsPerPage: number = 5;
  let totalPages: number = Math.ceil(jobs.length / itemsPerPage);

  let selectedJob: Job | null = null;
  selectedJob = jobs[0];

  // Получить вакансии для текущей страницы
  function getCurrentJobs(): Job[] {
    const start = (currentPage - 1) * itemsPerPage;
    const end = start + itemsPerPage;
    return jobs.slice(start, end);
  }

  function changePage(page: number) {
    if (page > 0 && page <= totalPages) {
      currentPage = page;
    }
  }

  // Функция для выбора вакансии
  function selectJob(job: Job) {
    selectedJob = job;
  }

  let isFiltersOpen = writable(false);

  function openFilters() {
    isFiltersOpen.set(true);
  }

  function closeFilters() {
    isFiltersOpen.set(false);
  }

  function applyFilters() {
    closeFilters();
    alert("Применены");
  }
</script>

<svelte:head>
  <title>itpq - Все вакансии</title>
</svelte:head>

<main class="flex-grow py-8 flex flex-col max-w-[1440px] mx-auto">
  <h1 class="text-4xl md:text-5xl font-bold text-center mb-6">Вакансии</h1>

  <div class="w-full flex items-center justify-center text-black">
    <input
      class="w-full max-w-[500px] h-[40px] bg-gray-300 px-[40px] rounded"
      placeholder="Поиск"
      type="text"
    />
  </div>

  <button
    on:click={openFilters}
    class="w-fit mb-5 p-2 bg-gray-300 text-gray-800 rounded-md hover:bg-gray-400"
  >
    Фильтры
  </button>

  <section class="flex gap-5 w-full">
    <div class="w-[40%]">
      {#each getCurrentJobs() as job}
        <button
          class="w-full text-left p-4 mb-4 border rounded-md dark:bg-gray-700 hover:dark:bg-gray-600 dark:text-white cursor-pointer"
          on:click={() => selectJob(job)}
        >
          <div class="flex justify-between">
            <div>
              <h2 class="text-xl font-bold">{job.title}</h2>
              <p class="text-sm">{job.company} - {job.location}</p>
              <p class="text-sm">{job.payment}</p>

              <div class="flex items-center gap-x-3 mt-2">
                <div class="bg-white text-black rounded px-3">Android</div>
                <div class="bg-white text-black rounded px-3">Kotlin</div>
              </div>
            </div>
            <div class="flex items-end">
              <p class="text-xs">1 день назад</p>
            </div>
          </div>
          <!-- <p class="mt-2">{job.description}</p> -->
        </button>
      {/each}
    </div>

    <div
      class="hidden md:block w-full p-4 mb-4 border rounded-md dark:bg-gray-700 dark:text-white"
    >
      {#if selectedJob}
        <div class="flex justify-between">
          <div>
            <h2 class="text-xl font-bold">{selectedJob.title}</h2>
            <p class="text-sm">
              {selectedJob.company} - {selectedJob.location}
            </p>
            <p class="text-2xl font-semibold">{selectedJob.payment}</p>
          </div>
          <div class="flex items-start gap-x-5">
            <button
              class="w-[40px] h-[40px] flex items-center justify-center bg-gray-300 rounded"
              type="button"
            >
              <img alt="dots" src="icons/dots.svg" />
            </button>

            <button
              class="w-[40px] h-[40px] flex items-center justify-center bg-gray-300 rounded"
              type="button"
            >
              <img alt="favorite" src="icons/favorite.svg" />
            </button>

            <div>
              <button
                class="h-[40px] px-3 flex items-center justify-center bg-green-500 rounded font-semibold"
                type="button"
              >
                Откликнуться на сайте компании
              </button>
              <p class="text-xs text-end mt-1">Вакансия размещена не на itpq</p>
            </div>
          </div>
        </div>

        <p class="text-base mb-2">{selectedJob.description}</p>
      {/if}
    </div>
  </section>

  {#if $isFiltersOpen}
    <div
      class="fixed inset-0 bg-gray-900 bg-opacity-80 flex justify-center items-center"
    >
      <div
        class="dark:bg-gray-800 p-6 rounded-md w-full max-w-md relative z-50"
      >
        <h2 class="text-2xl font-bold mb-4">Фильтры</h2>
        <form on:submit|preventDefault={applyFilters}>
          <label class="block mb-2">
            Зарплата:
            <input type="number" class="border p-2 w-full text-black rounded" />
          </label>

          <div class="flex justify-end mt-4">
            <button
              on:click={closeFilters}
              type="button"
              class="mr-2 bg-gray-300 text-gray-800 p-2 rounded-md hover:bg-gray-400"
              >Отмена</button
            >
            <button
              type="submit"
              class="bg-blue-500 text-white p-2 rounded-md hover:bg-blue-600"
              >Применить</button
            >
          </div>
        </form>
      </div>
    </div>
  {/if}
</main>
