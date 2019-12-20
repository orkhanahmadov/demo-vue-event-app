<template>
  <div id="app" class="px-10">
    <form @submit.prevent="submit">
      <div class="flex flex-wrap -mx-3 my-4">
        <div class="w-1/3 px-3">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="name">
            Name
          </label>

          <input v-model="form.name"
                 class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                 type="text"
                 placeholder="Name">
        </div>

        <div class="w-2/3 px-3">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="description">
            Description
          </label>

          <textarea v-model="form.description"
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
                 class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                 type="date"
                 placeholder="Date">
        </div>

        <div class="w-1/3 px-3">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="start_time">
            Start time
          </label>

          <input v-model="form.start_time"
                 class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                 type="time"
                 placeholder="Start time">
        </div>

        <div class="w-1/3 px-3">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="end_time">
            End time
          </label>

          <input v-model="form.end_time"
                 class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                 type="time"
                 placeholder="End time">
        </div>
      </div>

      <br />
      <button class="px-4 py-2 bg-blue-500 rounded text-white shadow hover:bg-blue-600">Create event</button>
    </form>

    <div v-for="event in events" :key="event.name" class="flex flex-wrap">
      <div class="flex-1">{{ event.name }}</div>
      <div class="flex-1">{{ event.description }}</div>
      <div class="flex-1">{{ event.date }}</div>
      <div class="flex-1">{{ event.start_time + ' - ' + event.end_time }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',

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
    requiredClass() {
      if (this.form.name === 'Orkhan') return 'text-green-700';

      return ''
    }
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
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
