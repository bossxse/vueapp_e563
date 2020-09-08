<template>
  <v-container>
    <form>
      <v-text-field
        v-model="std_id"
        :counter="10"
        label="รหัสนักศึกษา"
        required
      />
      <v-text-field
        v-model="name"
        :counter="10"
        label="ชื่อ"
        required
      />
      <v-text-field
        v-model="lname"
        label="นามสกุล"
        required
      />
      <v-select
        v-model="school_id"
        :items="items"
        label="รหัสสถานศึกษา"
        required
      />

      <v-btn class="mr-4" @click="submit">
        submit
      </v-btn>
      <v-btn @click="clear">
        clear
      </v-btn>
    </form>
    <div>
      <div class="text-center mb-4" />
      <v-alert
        :value="alert"
        color="pink"
        dark
        border="top"
        icon="mdi-home"
        transition="scale-transition"
      >
        ป้อนข้อมูลสำเร็จ
      </v-alert>
    </div>
    <div>
      <v-alert
        :value="alerterror"
        text
        outlined
        color="deep-orange"
        icon="mdi-fire"
      >
        ป้อนข้อมูลไม่สำเร็จ
      </v-alert>
    </div>
  </v-container>
</template>
<script>

export default {
  data: () => ({
    alert: false,
    alerterror: false,
    name: '',
    lname: '',
    std_id: '',
    school_id: '',
    items: [
      '1121100033',
      '1121100035',
      '1121100032',
      '1121100043',
      '1121100031',
    ],
    checkbox: null,
  }),

  methods: {
    async submit () {
      console.log('submit')
      try {
        let res = await fetch('http://localhost:7001/addStd?std_id=' + this.std_id +
                '&name=' + this.name + '&lname=' + this.lname +
                '&school_id=' + this.school_id + '')
        let data = await res.json()
        console.log('data', data)
        if (data.data[0] === 0) {
          this.alert = true
          this.alerterror = false
        }
      } catch (error) {
        this.alerterror = true
        this.alert = false
      }
    },
    clear () {
      this.name = ''
      this.lname = ''
      this.school_id = null
      this.std_id = ''
    },
  },
}
</script>
