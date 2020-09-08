<template>
  <v-container>
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
        label="นามสกุล"
      />
      <v-text-field
        v-model="is_active"
        label="สถานะ"
      />
      <v-btn class="mr-4" @click="submit">
        submit
      </v-btn>
      <v-btn @click="clear">
        clear
      </v-btn>
    </form>
  </v-container>
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
  methods: {
    async submit () {
      let res = await fetch('http://localhost:7001/insert?code=' + this.code + '&pre_name= ' + this.pre_name + '&first_name=' + this.first_name + '&last_name=' + this.last_name + '&is_active=' + this.is_active + '')
      let data = res.json()
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
