<template>
  <div class="mw-400">
    <h3 class="text-center m-3">Create page</h3>

    <div>
      <b-form @submit="create">
        <b-form-group id="input-group-1" label="User ID:" label-for="input-1">
          <b-form-input
            id="input-1"
            v-model="form.userId"
            type="text"
            placeholder="Enter User ID"
            required
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
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Post Body:" label-for="input-3">
          <b-form-textarea
            id="input-3"
            v-model="form.body"
            type="text"
            placeholder="Body"
            required
          ></b-form-textarea>
        </b-form-group>

        <div class="d-flex justify-content-around">
          <b-button type="submit" variant="primary">Submit</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
        </div>
        
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        userId: '',
        title: '',
        body: '',
      }
    }
  }, 
  methods: {
    create(e) { 
      e.preventDefault();
      fetch('https://jsonplaceholder.typicode.com/posts', {
        method: 'POST',
        body: JSON.stringify({
          title: this.form.title,
          body: this.form.body,
          userId: this.form.userId,
        }),
        headers: {
          'Content-type': 'application/json; charset=UTF-8',
        },
      })
      .then(() => {
        this.$router.push('/')
        console.log("post created")
      });
    }
  }
}
  
</script>

<style>
  .mw-400 {
    max-width: 400px;
    margin: 40px auto;
  }
  textarea.form-control {
    height: 150px !important;
  }
</style>