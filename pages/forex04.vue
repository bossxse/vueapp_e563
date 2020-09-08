<template>
  <v-card color="pink lighten-1">
    <center>
      <v-data-table
        :headers="headers"
        :items="students"
        :items-per-page="5"
        class="elevation-1"
      /> 
    </center>

    <v-card-text>
      <v-form>
        <v-text-field v-model="id" prepend-icon="mdi-account-circle" label="Username" />
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
      <v-btn @click="listStudent" color="success">
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
      id: '',
      pass: '',
      fname: '',
      headers: [
        {
          text: 'รหัสสถานศึกษา',
          align: 'start',
          sortable: false,
          value: 'school_id',    
        },
        { text: 'ชื่อ', value: 'name' },
        { text: 'นามสกุล', value: 'lastname' },
        { text: 'เพศ', value: 'gender' },
        { text: 'ชื่อสถานศึกษา', value: 'school_name' },
      ],
      students: [],
    }
  },
  // created() {
  //   this.listStudent()
  // },
  methods: {
    async  listStudent() {
      console.log('list std')
      let res = await fetch('http://localhost:7001/listStdex04?id=' + this.id)
      let data = await res.json()
      console.log('data',data.rows[0])
      this.students = data.rows[0]
      //console.log(data.rows.)
    },
  },
}
</script>
