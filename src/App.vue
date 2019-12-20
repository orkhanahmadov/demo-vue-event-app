<template>
  <div id="app" class="px-10">
    <form @submit.prevent="submit">
      <div class="flex flex-wrap -mx-3 my-4">
        <div class="w-1/3 px-3">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="name">
            Name
          </label>

          <input v-model="form.name"
                 id="name"
                 class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                 type="text"
                 placeholder="Name">

          <p v-if="showNameRequiredError" class="text-red-700 text-left text-sm mt-1">This field is required.</p>
          <p v-else-if="showNameLengthError" class="text-red-700 text-left text-sm mt-1">This field should have 3 or more characters.</p>
          <p v-else class="text-green-700 text-left text-sm mt-1">All good!</p>
        </div>

        <div class="w-2/3 px-3">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="description">
            Description
          </label>

          <textarea v-model="description"
                    id="description"
                    rows="3"
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    placeholder="Description">
          </textarea>
        </div>
      </div>

      <div class="flex flex-wrap -mx-3 my-4">
        <div class="w-1/3 px-3">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="date">
            Date
          </label>

          <input v-model="form.date"
                 id="date"
                 class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                 type="date"
                 placeholder="Date">
        </div>

        <div class="w-1/3 px-3">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="start_time">
            Start time
          </label>

          <input v-model="form.start_time"
                 id="start_time"
                 class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                 type="time"
                 placeholder="Start time">
        </div>

        <div class="w-1/3 px-3">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="end_time">
            End time
          </label>

          <input v-model="form.end_time"
                 id="end_time"
                 class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                 type="time"
                 placeholder="End time">
        </div>
      </div>
      <button class="block mx-auto px-4 py-2 rounded text-white mt-6"
              :class="disabledClass"
              :disabled="disableSubmit">Create event</button>
    </form>

    <event-list :events="events" @delete-event="deleteEvent" />
  </div>
</template>

<script>
import EventList from "./components/EventList";

export default {
  name: 'app',

  components: {
    EventList
  },

  data() {
    return {
      form: {
        name: '',
        description: '',
        date: '',
        start_time: '',
        end_time: '',
      },

      events: []
    }
  },

  computed: {
    description: {
      get() {
        return this.form.description
      },

      set(value) {
        this.form.description = value
      }
    },

    showNameRequiredError() {
      return !this.form.name
    },

    showNameLengthError() {
      return this.form.name.length < 3
    },

    disableSubmit() {
      return this.showNameRequiredError || this.showNameMinimumLengthError
    },

    disabledClass() {
      return this.disableSubmit
              ? 'cursor-not-allowed bg-gray-300'
              : 'bg-blue-500 hover:bg-blue-600 shadow'
    },
  },

  methods: {
    submit() {
      this.events.push({...this.form})
      this.form = {
        name: '',
        description: '',
        date: '',
        start_time: '',
        end_time: '',
      }
    },

    deleteEvent(index) {
      this.events.splice(index, 1)
    }
  }
}
</script>