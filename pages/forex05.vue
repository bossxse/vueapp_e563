<template>
  <div>
    <h1>Student List</h1>
    <ul>
      <li v-for="st in students" :key="st.code">
        <span>{{ st.GPA }}</span>
        <span>{{ st.name }}</span>
        <span>{{ st.lastname }}</span>
        <span>{{ st.school_name }}</span>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      students: '',
    }
  },
  created() {
    this.listStudent()
  },
  methods: {
    async  listStudent() {
      console.log('list std')
      let res = await fetch('http://localhost:7001/listStdex05')
      let data = await res.json()
      console.log('data',data.rows[0])
      this.students = data.rows[0]
      //console.log(data.rows.)
    },
  },
}
</script>
