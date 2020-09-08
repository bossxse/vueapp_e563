<template>
  <v-card color="pink lighten-1">
    <center>
      <v-data-table
        :headers="headers"
        :items="students"
        :items-per-page="5"
        class="elevation-1"
      /> 
      <h1>SIGN IN</h1><h2>{{ fname }}</h2>
    </center>

    <v-card-text>
      <v-form>
        <v-text-field v-model="user" prepend-icon="mdi-account-circle" label="Username" />
      </v-form>
    </v-card-text>
    <v-card-actions>
      <nuxt-link to="login">
        <v-btn color="primary">
          <v-icon>loupe</v-icon>
          Home
        </v-btn>
      </nuxt-link>
      <v-spacer />
      <!-- <nuxt-link to="menu"> -->
      <v-btn @click="doSave" color="success">
        <v-icon>forward</v-icon>
        search
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
      user: '',
      pass: '',
      fname: '',
      headers: [
        {
          text: 'NAME',
          align: 'start',
          sortable: false,
          value: 'name',    
        },
        { text: 'school_id', value: 'school_id' },
        { text: 'GPA', value: 'GPA' },
      ],
      students: [
        {
          name: "11",
          G: 11,
          ask2: 11,
        },
      ],

    }
  },
  methods: {
    async  doSave() {
      console.log('do Svae')
      let res = await fetch('http://localhost:7001/school?user=' + this.user + '&dep=it')
      let data = await res.json()
      this.students = data.row
      console.log('students = ', this.students)
    //   console.log(data.row.name)
    //   this.fname = data.row.name
    },
  },
}
</script>
