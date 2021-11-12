<template>
  <section>
    <b-table
      :data="items"
      :paginated="isPaginated"
      :per-page="perPage"
      :current-page.sync="currentPage"
      :pagination-simple="isPaginationSimple"
      :pagination-position="paginationPosition"
      :default-sort-direction="defaultSortDirection"
      :pagination-rounded="isPaginationRounded"
      :checked-rows.sync="checkedRows"
      checkable
      :checkbox-position="checkboxPosition"
      custom-row-key="id"
    >
      <b-table-column
        field="id"
        label="ID"
        width="40"
        :td-attrs="columnTdAttrs"
        numeric
        v-slot="props"
      >
        {{ props.row.id }}
      </b-table-column>

      <b-table-column
        field="first_name"
        label="First Name"
        :td-attrs="columnTdAttrs"
        v-slot="props"
      >
        {{ props.row.first_name }}
      </b-table-column>

      <b-table-column
        field="last_name"
        label="Last Name"
        :td-attrs="columnTdAttrs"
        v-slot="props"
      >
        {{ props.row.last_name }}
      </b-table-column>

      <b-table-column
        field="date"
        label="Date"
        :th-attrs="dateThAttrs"
        :td-attrs="columnTdAttrs"
        v-slot="props"
      >
        <span>
          {{ props.row.date }}
        </span>
      </b-table-column>

      <b-table-column label="Gender" :td-attrs="columnTdAttrs" v-slot="props">
        <span>
          <b-icon
            v-if="props.row.id !== 'Total'"
            pack="fas"
            :icon="props.row.gender === 'Male' ? 'mars' : 'venus'"
          >
          </b-icon>
          {{ props.row.gender }}
        </span>
      </b-table-column>

      <b-table-column
        field=""
        label=""
        v-slot="props"
        :td-attrs="columnTdAttrs"
      >
        <div class="flex">
          <section>
            <div class="buttons">
              <img
                style="margin-right: 16px; cursor: pointer"
                src="~/assets/Edit.svg"
                alt=""
                @click="addId(props.row.id)"
              />
            </div>

            <b-modal v-model="isCardModalActiveForm" :width="640" scroll="keep">
              <div class="card">
                <header class="modal-card-head">
                  <p class="modal-card-title">Edit Item</p>
                  <button
                    type="button"
                    class="delete"
                    @click="isCardModalActiveForm = false"
                  />
                </header>
                <div style="padding: 16px" class="">
                  <b-field>
                    <input @change="addFirst" placeholder="New first name" />
                  </b-field>

                  <b-field>
                    <input
                      @change="addSecond"
                      v-model="last_name"
                      placeholder="New last name"
                    />
                  </b-field>
                </div>

                <footer class="modal-card-foot">
                  <b-button
                    label="Close"
                    @click="isCardModalActiveForm = false"
                  />
                  <b-button
                    label="Save"
                    @click="updateItem()"
                    type="is-success"
                  />
                </footer>
              </div>
            </b-modal>
          </section>

          <section>
            <div class="buttons">
              <img
                src="~/assets/Delete.svg"
                style="cursor: pointer"
                alt=""
                @click="deleteItem(props.index)"
              />
            </div>
          </section>
        </div>
      </b-table-column>
      <template #bottom-left>
        <div class="flex">
          <p>Display</p>
          <b-select v-model="perPage" :disabled="!isPaginated">
            <option value="5">5</option>
            <option value="10">10</option>
            <option value="15">20</option>
            <option value="20">30</option>
          </b-select>
          <p>request per page</p>
        </div>
      </template>
    </b-table>
  </section>
</template>

<script>
export default {
  data() {
    const data = []
    return {
      data,
      id: null,
      first_name: '',
      last_name: '',
      log: console.log,
      isCardModalActive: false,
      isCardModalActiveForm: false,
      isPaginated: true,
      isPaginationSimple: false,
      isPaginationRounded: false,
      paginationPosition: 'bottom',
      defaultSortDirection: 'asc',
      sortIcon: 'arrow-up',
      sortIconSize: 'is-small',
      currentPage: 1,
      perPage: 5,
      checkboxPosition: 'left',
      checkedRows: [this.items[1]],
      columns: [
        {
          field: 'id',
          label: 'ID',
          width: '40',
          numeric: true,
        },
        {
          field: 'first_name',
          label: 'First Name',
        },
        {
          field: 'last_name',
          label: 'Last Name',
        },
        {
          field: 'date',
          label: 'Date',
        },
        {
          field: 'gender',
          label: 'Gender',
        },
      ],
    }
  },
  methods: {
    deleteItem(index) {
      const s = this.items.splice(index, 1)
      this.deleted()
      return s
    },
    deleted() {
      this.$buefy.toast.open({
        message: 'Item Deleted!',
        type: 'is-success',
      })
    },
    updated() {
      this.$buefy.toast.open({
        message: 'Item Deleted!',
        type: 'is-success',
      })
    },
    addFirst({ type, target }) {
      this.first_name = target.value
    },
    addSecond({ type, target }) {
      this.last_name = target.value
    },
    updateItem() {
      const elementsIndex = this.items.findIndex(
        (element) => element.id == this.id
      )
      let newArray = [...this.items]
      newArray[elementsIndex] = {
        ...newArray[elementsIndex],
        first_name: this.first_name,
        last_name: this.last_name,
      }
      this.items = newArray
      this.isCardModalActiveForm = false
      this.updated()
    },
    addId(id) {
      this.id = id
      this.isCardModalActiveForm = true
    },
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
}
</script>
