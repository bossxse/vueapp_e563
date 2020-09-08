<template>
  <v-data-table
    :headers="headers"
    :items="students"
    :items-per-page="5"
    class="elevation-1"
  />
</template>
<script>
export default {
  data () {
    return {
      headers: [
        {
          text: 'รหัสประจำตัว',
          align: 'start',
          sortable: false,
          value: 'code',
        },
        { text: 'ชื่อ - สกุล', value: 'first_name' },
        { text: 'สถานะ (g)', value: 'is _active' },
      ],
      students: [
        {
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
        },
      ],
    }
  },
  created () {
    this.showStd()
  },
  methods: {
    async showStd() {
      let res = await fetch('http://localhost:7001/showStd')
      let data = await res.json()
      console.log('data=', data)
      this.students = data.rows[0]
    },
  },
}
</script>