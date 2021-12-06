<template>
  <div class="accordion-item">
    <h2
      class="accordion-header"
      id="fall2019heading"
      v-b-toggle:[schedule.collapseId]
    >
      <div class="">
        <h4 class="my-0">{{ schedule.name }}</h4>
      </div>
    </h2>
    <b-collapse :id="schedule.collapseId">
      <div class="accordion-body">
        <table class="table table-hover">
          <thead>
            <th>Course</th>
            <td></td>
            <td></td>
            <th>Credits</th>
          </thead>
          <tr v-for="c in classes" :key="c.id">
            <td>{{ c["Course ID"] }}</td>
            <td>
              <span class="fw-bold">{{ c["Course Name"] }}</span>
            </td>
            <td>
              <span :class="getBadgeClass(c['Category'].toLowerCase())">{{
                c["Category"]
              }}</span>
            </td>
            <td>{{ c["Credit Hours"] }}</td>
          </tr>
          <tr>
            <td></td>
            <td></td>
            <td></td>
            <td class="fw-bold">{{ this.totalHours() }}</td>
          </tr>
        </table>
      </div>
    </b-collapse>
  </div>
</template>

<script>
export default {
  name: "SemesterSchedule",
  props: {
    schedule: Object,
    classes: Array,
  },
  methods: {
    totalHours() {
      // add all hours in table
      var total = 0;

      this.classes.forEach((c) => {
        total += parseInt(c["Credit Hours"]);
      });

      return total;
    },
    getBadgeClass(category) {
      if (category === "lac") {
        return "badge bg-primary";
      } else {
        return "badge bg-secondary";
      }
    },
  },
};
</script>

<style>
</style>