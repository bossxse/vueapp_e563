<template>
  <v-card color="pink lighten-1">
    <center>
      <v-data-table
        :headers="headers"
        :items="datas"
        :items-per-page="5"
        class="elevation-1"
      />
      <h1>โชว์ข้อมูล ข้อ 3 </h1><h2>{{ fname }}</h2>
    </center>

    <v-card-text>
      <v-form>
        <v-text-field v-model="gpa" prepend-icon="mdi-account-circle" label="(GPA)" />
        <v-text-field v-model="province_id" prepend-icon="mdi-account-circle" label="province_id" />
        <v-container fluid>
          <v-row align="center">
            <v-col class="d-flex" cols="12" sm="6">
              <v-select
                v-model="gender"
                :items="items"
                label="Standard"
              />
            </v-col>
          </v-row>
        </v-container>
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
      <v-btn @click="doSearch" color="success">
        <v-icon>forward</v-icon>
        LOGIN
      </v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  name: 'App',
  data () {
    return {
      showPassword: false,
      province: '',
      province_id: '',
      id: '',
      pass: '',
      fname: '',
      name: '',
      gpa: '',
      gender: '',
      headers: [
        {
          text: 'รหัสนักศึกษา',
          align: 'start',
          sortable: false,
          value: 'student_id',
        },
        { text: 'Name', value: 'name' },
        { text: 'GPA', value: 'GPA' },
        { text: 'gender', value: 'gender' },
        { text: 'province_name', value: 'province_name' },

      ],
      datas: [],
      items: ['m', 'f'],
    }
  },
  methods: {
    async doSearch() {
      console.log('doSearch')
      let res = await fetch('http://localhost:7001/w04?gpa=' + this.gpa + '&province_id=' + this.province_id + '&gender=' + this.gender)
      let data = await res.json()
      this.datas = data.rows
      console.log('data', data.rows)
    },
  },
  // created() {
  //   this.listStudent()
  // },
}
</script>
