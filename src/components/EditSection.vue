<template>
  <section class="add container">
    <div class="add-forms">
        <div class="row d-flex align-items-center" style="text-align: left;">
          <label class="add__label col-6">
            First Name
            <input
              v-model="form.firstName"
              class="add__input"
              type="text"
              placeholder="Ibrohim"
              required
            />
          </label>
          <label class="add__label col-6">
            Last Name
            <input
              v-model="form.lastName"
              class="add__input"
              type="text"
              placeholder="Olimjonov"
              required
            />
          </label>
        </div>
        <div class="row d-flex align-items-center" style="text-align: left;">
          <label class="add__label col-6">Interesting
            <select v-model="form.interesting" class="add__input col-11" required>
              <option disabled selected>Choose</option>
              <option value="IT">IT</option>
              <option value="Sport">Sport</option>
              <option value="Math & Accounting">Math & Accounting</option>
            </select>
          </label>
          <label class="add__label col-6">Class
            <input
              v-model="form.studentClass"
              class="add__input"
              type="text"
              placeholder="9-04"
              required
            />
          </label>
        </div>
    </div>
    <div class="add-details d-flex align-items-start flex-column">
      <div class="add-form mt-4 d-flex align-items-start flex-column">
        <h4 for="" class="add__label">Gender</h4>
        <div class="d-flex align-items-start gap-4">
          <div class="form-check d-flex align-items-baseline gap-2">
            <label for="Male" class="add__label">
              <input
                v-model="form.gender"
                type="radio"
                name="Gender"
                id="Male"
                class="add__check"
                value="Male"
                required
              />
            Male</label>
          </div>
          <div class="form-check d-flex align-items-baseline gap-2">
            <label for="Female" class="add__label">
              <input
              v-model="form.gender"
              type="radio"
              name="Gender"
              id="Female"
              class="add__check"
              value="Female"
              required
              />
              Female</label>
          </div>
        </div>
      </div>
      <div class="add-form mt-4" style="text-align: left;">
        <div class="row">
          <div class="col-6">
            <label for="" class="add__label">
              Data of Birth
              <input
              v-model="form.dataOfBirth"
              class="add__input"
              type="date"
              placeholder="dd/mm/yy"
              required
            />
            </label>
          </div>
        </div>
      </div>
    </div>
    <input
      @click="updateButton()"
      type="submit"
      class="button mt-4 d-flex align-items-start"
      value="Update and Save"
    />
  </section>
</template>

<script>
import {mapState} from 'vuex'

export default {
  name: "EditSection",
  data() {
    return {
      form: {},
      perPage: 2,
      currentPage: 2,
      employees: null,
      query: '',
    };
  },
  async created() {
    await this.$store.dispatch('LOAD_FROM_LOCALSTORAGE')
    let index = this.$route.params.index
    if (!/^\d+$/.test(index)) {
      return this.$router.push('/404')
    }
    index = parseInt(index)
    const items = this.$store.state.employees.items
    const item = items[index]
    if (!item) {
      return this.$router.push('/404')
    }
    this.form = Object.assign({}, item)
  },
  methods: {
    clearForm() {
      this.form = {};
    },
   async updateButton() {
    this.$store.commit('UPDATE_ITEM', {
    index: this.$route.params.index,
    student: this.form,
    })
    await this.$store.dispatch('SAVE_TO_LOCALSTORAGE')
    await this.$router.push('/employees')
    },
  },
   computed: {
    ...mapState({
      students: s => s.employees.students,
    }),
    countMale() {
      return this.students.filter(el => el.picked === 'male').length
    },
    countFemale() {
      return this.students.filter(el => el.picked === 'female').length
    },
    countAccounting() {
      return this.students.filter(el => el.selected === 'Math & Accounting').length
    },
    countIT() {
      return this.students.filter(el => el.selected === 'IT').length
    },
    countMarketing() {
      return this.students.filter(el => el.selected === 'sport').length
    },
  },
  mounted() {
    this.$store.dispatch('LOAD_FROM_LOCALSTORAGE')
  },
};
</script>

<style lang="scss">
.add {
  margin-top: 30px;
  .form-check {
    padding-left: 0;
  }
}
</style>
