<template>
  <div class="postavke">
      <div class="row">
        <div class="col-sm-3"></div>
        <div class="col-sm-6">
          <div class="card border-info mb-3">
            <h1 class="card-header text-info text-center mb-5">Promjena lozinke</h1>
            <div class="card-body">
              <form @submit.prevent="update">
                <div class="form-group col-md-12">
                  <label for="exampleInputPassword1"> Postojeća lozinka</label>
                  <input v-model="old_password" type="password" class="form-control" id="exampleInputPassword1" placeholder="Postojeća lozinka"/>
                </div>
                <div class="form-group col-md-12">
                  <label for="exampleInputPassword2">Nova lozinka</label>
                  <input v-model="new_password" type="password" class="form-control" id="exampleInputPassword2" placeholder="Nova lozinka"/>
                </div>
                <br/>
                <div class="text-center">
                  <button type="submit" class="button">Promijeni lozinku</button>
                </div>
              </form>
            </div>
          </div>
        </div>
        <div class="col"></div>
      </div>
  </div>
</template>

<script>
import { Auth } from '@/services';

export default {
  data() {
    return {
      username: '',
      old_password: '',
      new_password: ''
    };
  },
  methods: {
    async update() {
      let promjena_lozinke = {
        username: this.username,
        old_password: this.old_password,
        new_password: this.new_password
      };
      let success = await Auth.changePassword(promjena_lozinke);
      console.log("Promjena lozinke ", success);

      alert("Uspješna promjena lozinke!");
      if (success == true) {
        this.$router.push({ name: 'home' });
      }   
    }
  }
};
</script>

<style lang="scss">
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  margin-top:30px;
  margin-right: 30px;
}
.button {
  background-color: rgb(71, 170, 216);
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
.button:hover {
  background-color: rgb(30, 122, 165);
}
.postavke{
    padding-top: 100px;
}
</style>