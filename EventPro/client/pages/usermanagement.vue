<template>

  <FormSidebar></FormSidebar>

  <div class="mx-auto max-w-5xl py-10 pl-10">
    <h3 class="text-2xl font-bold">Users</h3>
    <div>

      <FormButton
        type="button"
        buttonStyle="primary"
        @click="navigateTo('/users/new')"
        >New User</FormButton>
    </div>
    <div>
      <div v-if="pending">Loading ...</div>
      <div v-else>
        <table class="min-w-full text-left text-sm font-light">
          <thead class="border-b font-medium dark:border-neutral-500">
            <tr>
              <th scope="col" class="px-6 py-2">Name</th>
              <th scope="col" class="px-6 py-2">Course</th>
              <th scope="col" class="px-6 py-2">Is Active</th>
              <th scope="col" class="px-6 py-2">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr
              class="border-b dark:border-neutral-500"
              v-for="user in users"
              :key="user.id"
            >
              <td class="whitespace-nowrap px-6 py-2 font-medium">
                {{ user.name }}
              </td>
              <td class="whitespace-nowrap px-6 py-2">{{ user.course }}</td>
              <td class="whitespace-nowrap px-6 py-2">
                <span v-if="user.is_active" class="text-green-700">✓</span>
                <span v-else class="text-red-700">X</span>
              </td>
              <td class="whitespace-nowrap px-6 py-2">
                <a
                  class="cursor-pointer hover:underline hover:text-gray-700"
                  @click="viewUser(user.id)"
                >
                  View
                </a>
                <a
                  class="cursor-pointer hover:underline hover:text-gray-700"
                  @click="editUser(user.id)"
                >
                  Edit
                </a>
              </td>
            </tr>
          </tbody>
        </table>
        <div>
          <button
            class="mr-5 bg-blue-700 hover:bg-blue-600 text-white font-bold py-2 px-6 rounded-lg mt-5"
            @click="previousPage"
            :disabled="currentPage === 1"
          >
            Previous
          </button>

          <button
            class="mr-5 bg-blue-700 hover:bg-blue-600 text-white font-bold py-2 px-6 rounded-lg"
            @click="nextPage"
            :disabled="currentPage === totalPages"
          >
            Next
          </button>
        </div>
      </div>
    </div>
  </div>


</template>

<script setup>

import { ref, onMounted } from "vue";

const currentPage = ref(1);
const perPage = 10; // Number of items to display per page
const totalPages = ref(0);
const users = ref([]);

onMounted(() => {
  fetchData();
});

function viewUser(userId) {
  navigateTo("/users/" + userId);
}

function editUser(userId) {
  navigateTo("/users/edit?user_id=" + userId);
}

async function previousPage() {
  if (currentPage.value > 1) {
    currentPage.value--;
    await fetchData();
  }
}

async function nextPage() {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
    await fetchData();
  }
}

async function fetchData() {
  const response = await fetch(
    `http://127.0.0.1:8000/api/users?page=${currentPage.value}&perPage=${perPage}`
  );
  const responseData = await response.json();
  users.value = responseData.data;
  totalPages.value = Math.ceil(responseData.total / perPage);
}
</script>
