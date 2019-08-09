<template>
  <div id="container">
    <div class="row">
      <!-- <div class=" col-md-3">

      </div> -->
      <div class="col-xs-12 col-sm-8 sm-offset-2 col-md-6 offset-md-3">
        <h1>Http</h1>
        <div class="form-group">
          <label for="">Username</label>
          <input type="text" name="" value="" class="form-control" v-model="user.username">

        </div>
        <div class="form-group">
          <label for="">Mail</label>
          <input type="text" name="" value="" class="form-control" v-model="user.email">

        </div>
        <button type="submit" name="button" class="btn btn-primary" @click="submit">Submit</button>
        <hr>
        <button type="submit" name="button" class="btn btn-primary" @click="fetchData">Get Data</button>
        <br><br>
        <ul class="list-group">
          <li class="list-group-item" v-for="u in users">{{ u.username }} - {{ u.email }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      user: {
        username: '',
        email: '',
      },
      users: []
    }
  },
  methods: {
    submit() {
      this.$http.post('https://udemy-practice-vuejs-app.firebaseio.com/data.json', this.user)
        .then(responce => {
          console.log(responce)
        }, error => {
          console.log(error)
        });
    },
    fetchData() {
      this.$http.get('https://udemy-practice-vuejs-app.firebaseio.com/data.json')
        .then(responce => {
          return responce.json();
        })
        .then(data => {
          const resultArray = [];
          for (let key in data) {
            resultArray.push(data[key]);
          }

            console.log(resultArray);
          this.users = resultArray;
        });
    }
  }
}
</script>

<style>

</style>
