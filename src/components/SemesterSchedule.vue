<template>
  <div class="accordion-item">
    <h2
      class="accordion-header"
      :id="schedule.id + 'heading'"
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
            <th id="hours">Credits</th>
            <td></td>
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
            <td id="hours">{{ c["Credit Hours"] }}</td>
            <td><b-icon id="remove" icon="trash" variant="danger" @click="$emit('remove-class', schedule, c)"></b-icon></td>
          </tr>
          <tr>
            <td></td>
            <td></td>
            <td></td>
            <td class="fw-bold" id="hours">{{ this.totalHours() }}</td>
            <td></td>
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

<style scoped>
#remove:hover {
  transform: scale(1.2);
  cursor: pointer;
  transition: 0.15s;
}

#hours {
  text-align: center;
}
</style>