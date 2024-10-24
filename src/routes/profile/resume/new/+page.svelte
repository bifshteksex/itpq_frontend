<script lang="ts">
  interface Resume {
    name: string;
    surname: string;
    patronymic: string;
    email: string;
    phone: string;
    jobTitle: string;
    skills: string;
    experience: string;
    gender: string;
    citizenships: string[];
  }

  let newResume: Resume = {
    name: "",
    surname: "",
    patronymic: "",
    email: "",
    phone: "",
    jobTitle: "",
    skills: "",
    experience: "",
    gender: "",
    citizenships: [""],
  };

  let step = 1;

  // Объект для хранения ошибок
  let errors = {
    name: "",
    surname: "",
    email: "",
    phone: "",
  };

  // Валидация для шага 1
  function validateBasicInfo() {
    let valid = true;
    // Очистка ошибок перед валидацией
    errors = {
      name: "",
      surname: "",
      email: "",
      phone: "",
    };

    if (!newResume.name) {
      errors.name = "Имя обязательно для заполнения";
      valid = false;
    }

    if (!newResume.surname) {
      errors.surname = "Фамилия обязательна для заполнения";
      valid = false;
    }

    return valid;
  }

  // Валидация для шага 2
  function validateContactInfo() {
    let valid = true;
    // Очистка ошибок перед валидацией
    errors.email = "";
    errors.phone = "";

    if (!newResume.email) {
      errors.email = "Email обязателен для заполнения";
      valid = false;
    }

    if (!newResume.phone) {
      errors.phone = "Телефон обязателен для заполнения";
      valid = false;
    }

    return valid;
  }

  // Переход к следующему шагу
  function nextStep() {
    // if (step === 1 && validateBasicInfo()) {
    step++;
  }

  // Возврат к предыдущему шагу
  function prevStep() {
    if (step > 1) {
      step--;
    }
  }

  // Добавить новое поле для гражданства
  function addCitizenship() {
    newResume.citizenships = [...newResume.citizenships, ""]; // Добавить пустую строку для нового гражданства
  }

  function selectGender(gender: string) {
    newResume.gender = gender;
  }

  // Функция для отправки формы
  function handleSubmit(event: Event) {
    event.preventDefault();
    if (validateContactInfo()) {
      console.log("Новое резюме:", newResume);

      // Очистка формы после отправки
      newResume = {
        name: "",
        surname: "",
        patronymic: "",
        email: "",
        phone: "",
        jobTitle: "",
        skills: "",
        experience: "",
        gender: "",
        citizenships: [""],
      };
      step = 1;
    }
  }
</script>

<main class="flex-grow py-8 flex flex-col w-full max-w-[1440px] mx-auto">
  <form
    class="w-full dark:bg-gray-800 p-6 shadow-md rounded flex flex-col items-center"
  >
    {#if step === 1}
      <!-- Шаг 1: Основная информация -->
      <div class="flex flex-col">
        <h3 class="text-3xl font-bold mb-5">Основная информация</h3>

        <div class="flex items-start gap-x-5">
          <div>
            <label for="surname" class="block text-white mb-2">Фамилия</label>
            <input
              type="text"
              id="surname"
              bind:value={newResume.surname}
              class="w-full p-2 border rounded-md text-black"
              required
            />
            {#if errors.surname}
              <span class="text-red-500 text-sm">{errors.surname}</span>
            {/if}
          </div>

          <div>
            <label for="name" class="block text-white mb-2">Имя</label>
            <input
              type="text"
              id="name"
              bind:value={newResume.name}
              class="w-full p-2 border rounded-md text-black"
              required
            />
            {#if errors.name}
              <span class="text-red-500 text-sm">{errors.name}</span>
            {/if}
          </div>

          <div>
            <label for="patronymic" class="block text-white mb-2"
              >Отчество (если есть)</label
            >
            <input
              type="text"
              id="patronymic"
              bind:value={newResume.patronymic}
              class="w-full p-2 border rounded-md text-black"
            />
          </div>
        </div>

        <div class="mt-5">
          <label for="gender" class="block text-white mb-2">Пол</label>
          <div class="flex items-center gap-x-5">
            <button
              type="button"
              class="rounded px-3 py-2"
              on:click={() => selectGender("male")}
              class:bg-blue-500={newResume.gender === "male"}
              class:bg-slate-400={newResume.gender !== "male"}
            >
              Мужской
            </button>
            <button
              type="button"
              class="rounded px-3 py-2"
              on:click={() => selectGender("female")}
              class:bg-pink-500={newResume.gender === "female"}
              class:bg-slate-400={newResume.gender !== "female"}
            >
              Женский
            </button>
          </div>
        </div>

        <div class="mt-5">
          <label for="birth" class="block text-white mb-2">Дата рождения</label>
          <input
            type="date"
            id="birth"
            class="w-full p-2 border rounded-md text-black"
            required
          />
        </div>

        <div class="mt-5">
          <label for="accommodation" class="block text-white mb-2"
            >Место проживания</label
          >
          <input
            type="text"
            id="accommodation"
            class="w-full p-2 border rounded-md text-black"
          />
        </div>

        <div class="mt-5">
          <label class="block text-white mb-2">Гражданство</label>

          {#each newResume.citizenships as citizenship, index}
            <input
              type="text"
              bind:value={newResume.citizenships[index]}
              class="w-full p-2 border rounded-md text-black mb-2"
              placeholder="Введите гражданство"
              required
            />
          {/each}

          <button
            type="button"
            class="rounded px-3 py-2 bg-slate-400 mt-3"
            on:click={addCitizenship}
          >
            + Добавить гражданство
          </button>
        </div>
      </div>

      <div class="w-full mt-4 flex justify-end">
        <button
          type="button"
          class="bg-blue-500 text-white px-4 py-2 rounded"
          on:click={nextStep}>Далее</button
        >
      </div>
    {/if}

    {#if step === 2}
      <!-- Шаг 2: Контактная информация -->
      <div class="flex flex-col">
        <h3 class="text-3xl font-bold mb-5">Контактная информация</h3>

        <div class="flex flex-col gap-y-5">
          <div>
            <label for="email" class="block text-white mb-2">Email</label>
            <input
              type="email"
              id="email"
              bind:value={newResume.email}
              class="w-full p-2 border rounded-md text-black"
              required
            />
            {#if errors.email}
              <span class="text-red-500 text-sm">{errors.email}</span>
            {/if}
          </div>

          <div>
            <label for="phone" class="block text-white mb-2">Телефон</label>
            <input
              type="tel"
              id="phone"
              bind:value={newResume.phone}
              class="w-full p-2 border rounded-md text-black"
              required
            />
            {#if errors.phone}
              <span class="text-red-500 text-sm">{errors.phone}</span>
            {/if}
          </div>
        </div>
      </div>

      <div class="w-full mt-4 flex justify-between">
        <button
          type="button"
          class="bg-gray-500 text-white px-4 py-2 rounded"
          on:click={prevStep}>Назад</button
        >
        <button
          type="button"
          class="bg-blue-500 text-white px-4 py-2 rounded"
          on:click={nextStep}>Далее</button
        >
        <!-- <button
          type="submit"
          class="bg-blue-500 text-white px-4 py-2 rounded"
          on:click|preventDefault={handleSubmit}>Сохранить</button
        > -->
      </div>
    {/if}

    {#if step === 3}
      <!-- Шаг 3: Образование -->
      <div class="flex flex-col">
        <h3 class="text-3xl font-bold mb-5">Образование</h3>

        <div class="flex flex-col gap-y-5">
          <button class="bg-gray-500 px-5 py-2 rounded">Среднее</button>
          <button class="bg-gray-500 px-5 py-2 rounded"
            >Среднее специальное</button
          >
          <button class="bg-gray-500 px-5 py-2 rounded"
            >Неоконченное высшее</button
          >
          <button class="bg-gray-500 px-5 py-2 rounded">Высшее</button>
          <button class="bg-gray-500 px-5 py-2 rounded">Бакалавр</button>
          <button class="bg-gray-500 px-5 py-2 rounded">Магистр</button>
          <button class="bg-gray-500 px-5 py-2 rounded">Кандидат наук</button>
          <button class="bg-gray-500 px-5 py-2 rounded">Доктор наук</button>
        </div>
      </div>

      <div class="w-full mt-4 flex justify-between">
        <button
          type="button"
          class="bg-gray-500 text-white px-4 py-2 rounded"
          on:click={prevStep}>Назад</button
        >
        <button
          type="button"
          class="bg-blue-500 text-white px-4 py-2 rounded"
          on:click={nextStep}>Далее</button
        >
      </div>
    {/if}
  </form>
</main>
