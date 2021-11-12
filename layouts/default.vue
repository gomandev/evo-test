<template>
  <div>
    <Navbar />
    <div class="main-flex">
      <Sidebar />
      <div class="main-body">
        <div class="top" style="display: flex">
          <Title>Test</Title>
          <img style="margin-left: 10px" src="~assets/ask.svg" alt="" />
        </div>
        <p class="subtitle">Select requests to perform actions</p>
        <Table :items="data" />

        <section>
          <b-field style="margin-top: 16px" custom-class="is-full">
            <b-upload v-model="dropFiles" @input="getFileData()" drag-drop>
              <section class="section">
                <div class="content has-text-centered">
                  <div
                    class="flex"
                    style="justify-content: center; align-items: center"
                  >
                    Drop files here or
                    <span class="file-cta" style="margin-left: 10px">
                      <span class="file-label" style="color: #32b3a7"
                        >Browse</span
                      >
                    </span>
                  </div>
                  <p>
                    <img
                      src="~/assets/Upload.svg"
                      style="cursor: pointer"
                      alt=""
                    />
                  </p>
                  <p style="font-size: 12px">
                    Also you can upload your data through SFTP |
                    <a style="color: #32b3a7" href="">Learn more</a>
                  </p>
                </div>
              </section>
            </b-upload>
          </b-field>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '../components/block/Navbar.vue'
import Sidebar from '../components/block/Sidebar.vue'
import Table from '../components/block/Table.vue'
import FileUpload from '../components/block/FileUpload.vue'
import Title from '../components/atom/Title.vue'
export default {
  components: {
    Navbar,
    Sidebar,
    Title,
    Table,
    FileUpload,
  },
  computed: {},
  data() {
    const data = [
      {
        id: 1,
        first_name: 'Jesse',
        last_name: 'Simmons',
        date: '2016-10-15 13:43:27',
        gender: 'Male',
      },
      {
        id: 2,
        first_name: 'John',
        last_name: 'Jacobs',
        date: '2016-12-15 06:00:53',
        gender: 'Male',
      },
      {
        id: 3,
        first_name: 'Tina',
        last_name: 'Gilbert',
        date: '2016-04-26 06:26:28',
        gender: 'Female',
      },
      {
        id: 4,
        first_name: 'Clarence',
        last_name: 'Flores',
        date: '2016-04-10 10:28:46',
        gender: 'Male',
      },
      {
        id: 5,
        first_name: 'Anne',
        last_name: 'Lee',
        date: '2016-12-06 14:38:38',
        gender: 'Female',
      },
    ]

    return {
      items: [
        {
          title: 'Home',
          icon: 'home',
          to: { name: 'index' },
        },
        {
          title: 'Inspire',
          icon: 'lightbulb',
          to: { name: 'inspire' },
        },
      ],
      dropFiles: null,
      log: console.log,
      data,
    }
  },
  methods: {
    deleteDropFile(index) {
      this.dropFiles.splice(index, 1)
    },
    success() {
      this.$buefy.toast.open({
        message: 'Items Added!',
        type: 'is-success',
      })
    },
    getFileData() {
      const reader = new FileReader()
      reader.onload = function (evt) {
        const parsedJSON = JSON.parse(evt.target.result)
        let newArray = [...this.data]
        newArray.push(...parsedJSON)
        this.data = newArray
      }.bind(this)
      reader.readAsText(this.dropFiles)
      this.success()
    },
  },
}
</script>
