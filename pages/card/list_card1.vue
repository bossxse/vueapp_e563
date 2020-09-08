<template>
  <div>
    <div>
      <h1>Card List</h1>
      <ul>
        <li v-for="cards in card" :key="cards.card_code">
          <span>{{ cards.card_code }}</span>
          <span>{{ cards.ref_type }}</span>
          <span>{{ cards.ref_code }}</span>
          <span>{{ cards.register_date }}</span>
          <span>{{ cards.is_active }}</span>
          <v-btn @click="edit(cards.card_code)">
            EDIT
          </v-btn>
          <!-- <v-btn @click="del(cards.card_code)">
            Delete
          </v-btn> -->
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
      card: [],
    }
  },
  created() {
    this.listcard()
  },
  methods: {
    async listcard() {
      console.log('list')
      let res = await fetch('http://localhost:7001/listcard')
      let data = await res.json()
      console.log('data=', data)
      this.card = data.rows
    },
    edit(card_code) {
      console.log('code=', card_code)
      this.$router.push('list_edit1_card?card_code=' + card_code)
    },
    // async del(code) {
    //   console.log('code=', code)
    //   let res = await this.$http.get('http://localhost:7001/del?code=' + code)
    //   console.log(res.data.status)
    //   if ( res.data.status = 'ok') {
    //     this.$router.push('list_std3')
    //   }
    // },
  },
}
</script>
