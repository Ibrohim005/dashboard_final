<template>
  <section class="add container">
    <form action="">
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
      @click="save()"
      type="submit"
      class="button mt-4 d-flex align-items-start"
      value="Submit Form"
    />
    </form>
  </section>
</template>

<script>
export default {
  name: "Add",
  data() {
    return {
      form: {
          firstName: "",
          lastName: "",
          interesting: "",
          studentClass: "",
          gender: "",
          dataOfBirth: "",
      },
    };
  },
  methods: {
    save() {
      if (
        this.form.firstName.length == 0 ||
        this.form.lastName.length == 0 ||
        this.form.interesting.length == 0 ||
        this.form.studentClass.length == 0 ||
        this.form.dataOfBirth.length == 0
      ){
        alert('Fill in the blanks!');
        return false;
      } else {
        this.$store.commit("getStudents", this.form);
        console.log(this.$store.state.students);
        this.$store.dispatch("saveDataToLocalStorage");
        this.form = {}
      }
    },
  },
};
</script>

<style lang="scss">
.add {
  margin-top: 30px;
  &__label {
    font-weight: 700 !important;
    margin-bottom: 6px;
    
  }
  &__input {
    padding: 0.375rem 0.75rem;
    width: 100%;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    outline: none;
    transition: all 0.3s;
    &:focus {
      box-shadow: 0 0 5px 4px #d64933;
    }
  }
  .form-check {
    padding-left: 0;
  }
}
</style>
