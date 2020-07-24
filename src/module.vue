<template>
  <section>
    <h1 class="type-title">Build App</h1>

    <p>
      <label for="method">Method</label>

      <select v-model="settings.method" id="method">
        <option value="GET">Get</option>
        <option value="POST">Post</option>
      </select>

      <label for="url">Url</label>
      <input v-model="settings.url" id="url" />
      <br />
      <button @click="save">Save</button>
    </p>

    <p>
      <button class="action" @click="deploy">Deploy</button>
    </p>
  </section>
</template>

<script>
const KEY = 'awh:all'

export default {
  name: 'AWH',
  data() {
    return {
      id: null,
      settings: {
        url: '',
        method: 'GET',
      },
    }
  },
  methods: {
    async save() {
      if (this.id)
        await this.$api.api.request('patch', '/settings/' + this.id, {}, { value: JSON.stringify(this.settings) })
    },
    async deploy() {
      const response = await fetch(this.settings.url, { method: this.settings.method })
      console.log(response)
    },
  },
  async mounted() {
    const { data } = await this.$api.api.request('get', '/settings', {}, {})
    const saved = Object.values(data).find((s) => s.key === KEY)
    if (!saved) await this.$api.api.request('post', '/settings', {}, { key: KEY, value: JSON.stringify(this.settings) })
    else {
      try {
        this.settings = JSON.parse(saved.value)
        this.id = saved.id
      } catch {}
    }
  },
}
</script>

<style lang="scss" scoped>
section {
  padding: 1em;
  color: var(--input-text-color);
}

p {
  margin: 1em 0;
}

button {
  appearance: none;
  padding: 0.5em 1em;
  background-color: var(--action);
  border-radius: var(--border-radius);
}

button.action {
  background-color: var(--action);
}

input,
select {
  appearance: none;
  border-radius: var(--border-radius);
  background-color: transparent;
  border: var(--input-border-width) solid var(--input-border-color);
  padding: 0.75em;
  margin-bottom: 1em;
}

input {
  width: 100%;
}

label {
  font-size: 1.25em;
  margin-bottom: 0.25em;
}
</style>
