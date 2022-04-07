<template>
  <div class="mw-400">
    <h3 class="text-center m-3">Edit Post</h3>

    <div>
      <b-form @submit="update">
        <b-form-group id="input-group-1" label="User ID:" label-for="input-1">
          <b-form-input
            id="input-1"
            v-model="form.userId"
            type="text"
            placeholder="Enter User ID"
            ></b-form-input>
          </b-form-group>

        <b-form-group
          id="input-group-2"
          label="Post Title:"
          label-for="input-2"
        >
          <b-form-input
            id="input-2"
            v-model="form.title"
            type="text"
            placeholder="Title"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Post Body:" label-for="input-3">
          <b-form-textarea
            id="input-3"
            v-model="form.body"
            type="text"
            placeholder="Body"
          ></b-form-textarea>
        </b-form-group>

        <div class="d-flex justify-content-around">
          <b-button type="submit" variant="primary">Submit</b-button>
          <nuxt-link :to="{ path: 'details', query: { id: form.id }}" class="btn btn-info">Cancel</nuxt-link>
        </div>
        
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {}
    }
  },
  async fetch () {
    this.form = await fetch(
      'https://jsonplaceholder.typicode.com/posts/'+this.$nuxt._route.query.id
    ).then(res => res.json())
    console.log(this.form.id)
  },
  methods: {
    update(e) { 
      e.preventDefault();
      fetch('https://jsonplaceholder.typicode.com/posts/'+this.$nuxt._route.query.id, {
        method: 'PUT',
        body: JSON.stringify({
          title: this.form.title,
          body: this.form.body,
          userId: this.userId,
        }),
        headers: {
          'Content-type': 'application/json; charset=UTF-8',
        },
      })
        .then(() => {
        this.$router.push({ path: 'details', query: { id: this.form.id } })
        console.log("post updated")
      });
    }
  }
}
</script>

<style>
  textarea.form-control {
    height: 150px !important;
  }
</style>