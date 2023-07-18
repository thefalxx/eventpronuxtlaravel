<template>
    <div class="mx-auto max-w-5xl py-10">
        <h3 class="text-2xl">Add User</h3>
        <div class="py-3">
            <button @click="back()" class="border px-4 py-1 hover:bg-gray-50">Back</button>
        </div>
        <div>
            <form class="space-y-3" @submit.prevent="saveUser()">
                <div>
                    <FormLabel label="Name" />
                    <FormTextField name="name" placeholder="Name" v-model="state.user.name" />
                </div>
                <div>
                    <FormLabel label="Email" />
                    <FormTextField name="email" placeholder="Email" v-model="state.user.email" />
                </div>
                <div>
                    <FormLabel label="Password" />
                    <FormTextField type="password" name="password" placeholder="Password" v-model="state.user.password" />
                </div>
                <div>
                    <FormLabel label="Status" />
                    <br />
                    <FormCheckbox :value="state.user.is_active ? true : false"
                        @click="state.user.is_active = !state.user.is_active" />
                </div>
                <div>
                    <FormButton type="submit" buttonStyle="primary" class="w-full">Save</FormButton>
                </div>
            </form>
        </div>
    </div>
</template>
  
<script setup>
const state = reactive({
    user: {
        name: null,
        password: null,
        email: null,
        is_active: false,
    }
})

function back() {
    navigateTo('/')
}

async function saveUser() {
    const payload = {
        name: state.user.name,
        email: state.user.email,
        password: state.user.password,
        is_active: state.user.is_active,
    }
    await $fetch(`http://127.0.0.1:8000/api/users`, {
        method: 'POST',
        body: payload
    }).then((result) => {
        if (result) {
            alert('Successfully saved.')
        }
    }).catch((error) => {
        alert('Something went wrong.')
    })
}
</script>