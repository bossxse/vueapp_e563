<template>
  <form>
    <v-text-field
      v-model="code"
      label="รหัส"
    />
    <v-text-field
      v-model="pre_name"
      label="คำนำหน้า"
    />
    <v-text-field
      v-model="first_name"
      label="ชื่อ"
    />
    <v-text-field
      v-model="last_name"
      label="สกุล"
    />
    <v-text-field
      v-model="is_active"
      label="สถานะ"
    />
    <v-btn class="mr-4" @click="saveStd">
      save
    </v-btn>
    <v-btn @click="clear">
      clear
    </v-btn>
  </form>
</template>

<script>
export default {
  data: () => ({
    code: '',
    pre_name: '',
    first_name: '',
    last_name: '',
    is_active: '',
  }),
  async created() {
    console.log('code_edit=', this.$route.query.code) // req.query.code
    let code = this.$route.query.code
    let res = await fetch('http://localhost:7001/editstd?code=' + code)
    let data = await res.json()
    console.log('api_send', data.row[0].code)
    this.code = data.row[0].code
    this.pre_name = data.row[0].pre_name
    this.first_name = data.row[0].first_name
    this.last_name = data.row[0].last_name
    this.is_active = data.row[0].is_active
  },
  methods: {
    async submit () {
      let res = await fetch('http://localhost:7001/insert?code=' + this.code + '&pre_nam=' + this.pre_name + '&first_name=' + this.first_name + '&last_name=' + this.last_name + '&is_active=' + this.is_active + '')
      let data = res.json()
    },
    async saveStd() {
      console.log('saveStd')
      let student = {
        code: this.code,
        pre_name: this.pre_name,
        first_name: this.first_name,
        last_name: this.last_name,
        is_active: this.is_active,
      }
      let res = await fetch('http://localhost:7001/addstd3', {
        method: 'post',
        headers: {
          'content-type': 'application/json',
        },
        body: JSON.stringify(student),
      })
      let data = await res.json()
      console.log('data=', data)
    },
    clear () {
      this.code = ''
      this.pre_name = ''
      this.first_name = ''
      this.last_name = ''
      this.is_active = ''
    },
  },
}
</script>
