<template>
    <div class="mx-auto max-w-5xl py-10">
        <h3 class="text-2xl">Edit User</h3>
        <div class="py-3">
            <button @click="back()" class="border px-4 py-1 hover:bg-gray-50">Back</button>
        </div>
        <div v-if="pending">
            Loading...
        </div>
        <div v-else>
            <form class="space-y-3" @submit.prevent="updateUser()">
                <div>
                    <FormLabel label="Name" />
                    <FormTextField name="name" placeholder="Name" v-model="state.user.name" />
                </div>
                <div>
                    <FormLabel label="Status" />
                    <br />
                    <FormCheckbox :value="state.user.is_active ? true : false"
                        @click="state.user.is_active = !state.user.is_active" />
                </div>
                <div>
                    <FormButton type="submit" buttonStyle="primary" class="w-full">Update</FormButton>
                </div>
            </form>
        </div>
    </div>
</template>
  
<script setup>
const route = useRoute();
const userId = route.query.user_id

const { pending, data: user } = await useLazyAsyncData('user', () => $fetch(`http://127.0.0.1:8000/api/users/${userId}`))

const state = reactive({
    user: {
        name: user && user.value && user.value.name,
        course: user && user.value && user.value.course,
        is_active: user && user.value && user.value.is_active,
    }
})

watch(user, (newData) => {
    state.user = {
        name: newData && newData.name,
        course: newData && newData.course,
        is_active: newData && newData.is_active,
    }
})

function back() {
    navigateTo('/')
}

async function updateUser() {
    const payload = {
        name: state.user.name,
        course: state.user.course,
        is_active: state.user.is_active,
    }
    await $fetch(`http://127.0.0.1:8000/api/users/${userId}`, {
        method: 'PUT',
        body: payload
    }).then((result) => {
        if (result) {
            alert('Successfully updated.')
        }
    })
}
</script>