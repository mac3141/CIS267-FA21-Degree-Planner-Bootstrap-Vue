<template>
  <div class="card my-2">
    <div class="card-body">
      <div class="row">
        <h5 class="col-9">
          <b>{{ course["Course Name"] }}</b>
        </h5>
        <p class="col-3 text-right">{{ course["Credit Hours"] }} hours</p>
      </div>

      <div class="row">
        <div class="col-8">
          <p class="card-subtitle">{{ course["Course ID"] }}</p>
        </div>
        <div class="col-4 text-right">
          <span class="text-muted">{{ course["Semester Offered"] }}</span>
        </div>
      </div>
      <div class="row">
        <b-form-select v-model="selected" :options="options"></b-form-select>

        <b-button block variant="outline-secondary" class="my-2" @click="emitAdd()">Add</b-button>
      </div>

      <div class="row">
        <div class="col">
          <a class="card-link fw-light" v-b-toggle="convertID(course['Course ID'])"
            >Course description ›</a
          >
        </div>
      </div>

      <b-collapse class="course-description collapse card-text" :id="convertID(course['Course ID'])">
        <p class="text-muted card-text">{{ course["Course Description"] }}</p>
      </b-collapse>
    </div>
  </div>
</template>

<script>
export default {
  name: "CourseInfo",
  props: {
    course: Object,
  },
  data() {
    return {
      options: [
        { value: null, text: "Please select an option" },
        { value: "fall2019", text: "Fall 2019" },
        { value: "spring2020", text: "Spring 2020" },
      ],
      selected: null,
    }
  },
  methods: {
    convertID(courseID) {
      return courseID.replace(" ", "").replace("/", "-").toLowerCase();
    },
    emitAdd() {
      console.log("click");
      this.$emit("add-course", this.selected, this.course);
    }
  },
};
</script>

<style>
a:hover {
  cursor: pointer;
}
</style>