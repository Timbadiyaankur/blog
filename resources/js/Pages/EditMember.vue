<template>
  <app-layout title="Dashboard">
    <template #header>
      <div class="flex">
        <div class="mx-auto ml-0">
          <h2 class="font-semibold text-xl text-gray-800 leading-tight">Edit Member</h2>
        </div>
      </div>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg p-6">
          <form @submit.prevent="submit">
            <div>
              <jet-label for="email" value="Email" />
              <jet-input id="email" v-model="form.email" type="email" class="mt-1 block w-full" required autofocus />
            </div>

            <div class="mt-4">
              <jet-label for="name" value="Name" />
              <jet-input id="name" v-model="form.name" type="text" class="mt-1 block w-full" required />
            </div>

            <div class="mt-4">
              <jet-label for="avatar" value="Avatar" />
              <jet-input id="avatar" type="file" class="mt-1 block w-full" @change="previewImage" />
            </div>

            <div class="mt-4">
              <img v-if="url" :src="url" class="mt-4 h-60" />
            </div>

            <div class="mt-4">
              <jet-button> Save </jet-button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
import AppLayout from '@/Layouts/AppLayout.vue'
import JetLabel from '@/Jetstream/Label.vue'
import JetInput from '@/Jetstream/Input.vue'
import JetButton from '@/Jetstream/Button.vue'

export default {
  name: 'EditMember',

  components: {
    AppLayout,
    JetLabel,
    JetInput,
    JetButton,
  },

  props: ['member'],

  data() {
    return {
      url: this.member.avatar,
      form: this.$inertia.form({
        email: this.member.email,
        name: this.member.name,
        id: this.member.id,
        avatar: null,
      }),
    }
  },
  mounted() {
    console.log(this.member)
  },
  methods: {
    submit() {
      this.form.post(this.route('edit-member'))
    },
    previewImage(e) {
      const file = e.target.files[0]
      this.form.avatar = file
      this.url = URL.createObjectURL(file)
    },
  },
}
</script>
