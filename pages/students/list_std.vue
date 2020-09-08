<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="student"
      :items-per-page="5"
      class="elevation-1"
    />
    <v-btn @click="listStd">
      click liststd
    </v-btn>
  </div>
</template>

<script>
export default {
  data () {
    return {
      headers: [
        {
          text: 'รหัส',
          align: 'start',
          sortable: false,
          value: 'code',
        },
        { text: 'ชื่อ', value: 'first_name' },
        { text: 'สกุล', value: 'last_name' },
        { text: 'สถานะ', value: 'is_active' },
      ],
      student: [
        {
          name: '123456',
          calories: 'alongkorn',
          fat: 'phukongka',
          carbs: 'Y',

        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,

        },
      ],
    }
  },
  methods: {
    async  listStd() {
      console.log('liststd')
      let res = await fetch('http://localhost:7001/liststd')
      let data = await res.json()
      console.log('data=', data)
      this.student = data.rows
    },
  },
}
</script>
