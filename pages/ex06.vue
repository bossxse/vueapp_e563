<template>
  <v-card color="pink lighten-1">
    <center>
      <v-icon size="120" color="rainbow">
        looks
      </v-icon>
      <h1>ค้นหาชื่อวิทยาลัย</h1><h2>{{ fname }}</h2>
    </center>

    <v-card-text>
      <v-form>
        <v-text-field v-model="id" prepend-icon="mdi-account-circle" label="รหัสสถานศึกษา" />
        <v-text-field v-model="gpa" prepend-icon="mdi-account-circle" label="GPA" />
      </v-form>
    </v-card-text>
    <v-card-actions>
      <nuxt-link to="register">
        <v-btn color="primary">
          <v-icon>loupe</v-icon>
          REGISTER
        </v-btn>
      </nuxt-link>
      <v-spacer />
      <!-- <nuxt-link to="menu"> -->
      <v-btn @click="doSave" color="success">
        <v-icon>forward</v-icon>
        LOGIN
      </v-btn>
      </nuxt-link>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  name: 'App',
  data () {
    return {
      showPassword: false,
      id: '',
      pass: '',
      fname: '',
      name: '',
      gpa: '',
    }
  },
  methods: {
    async  doSave() {
      console.log('do Save')
      let res = await fetch('http://localhost:7001/listex06?id=' + this.id + '&gpa=' + this.gpa)
      let data = await res.json()
      console.log(data)
      //console.log(data.rows.school_name)
      //this.fname = data.rows.school_name;
    },
  },
}
</script>
