<template>
  <div>
    <div>
      <h1>Student List</h1>
      <ul>
        <li v-for="std in student" :key="std.code">
          <span>{{ std.code }}</span>
          <span>{{ std.first_name }}</span>
          <span>{{ std.last_name }}</span>
          <span>{{ std.is_active }}</span>
          <v-btn @click="edit(std.code)">
            EDIT
          </v-btn>
          <v-btn @click="del(std.code)">
            Delete
          </v-btn>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      headers: [
        {
          text: 'รหัสนักศึกษา',
          align: 'start',
          sortable: false,
          value: 'code',
        },
        { text: 'ชื่อ', value: 'first_name' },
        { text: 'นามสกุล', value: 'last_name' },
        { text: 'สถานะ', value: 'is_active' },
      ],
      student: [],
    }
  },
  created() {
    this.listStd()
  },
  methods: {
    async listStd() {
      console.log('list')
      let res = await fetch('http://localhost:7001/liststd')
      let data = await res.json()
      console.log('data=', data)
      this.student = data.rows
    },
    edit(code) {
      console.log('code=', code)
      this.$router.push('list_edit3_std?code=' + code)
    },
    async del(code) {
      console.log('code=', code)
      let res = await this.$http.get('http://localhost:7001/del?code=' + code)
      console.log(res.data.status)
      if ( res.data.status = 'ok') {
        this.$router.push('list_std3')
        
      }
    },
  },
}
</script>
