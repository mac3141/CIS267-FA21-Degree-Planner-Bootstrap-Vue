<template>
  <div id="app" class="d-flex flex-column min-vh-100">
    <!-- Main Content -->
    <main class="flex-fill">
      <div class="container-fluid">
        <div class="row mb-5">
          <h1>Degree Planner</h1>
        </div>
        <div class="row main-content">
          <!-- Classes -->
          <div class="col-lg-4 required-classes">
            <h3>Required Classes</h3>

            <b-tabs content-class="mt-3">
              <!-- LAC Requirements -->

              <b-tab title="LAC" active>
                <div id="lac">
                  <div class="my-4 text-left" id="lac-reqs">
                    <!-- <div class="card my-2">
                      <div class="card-body">
                        <div class="row">
                          <h5 class="col-9">
                            <b>Life of Christ</b>
                          </h5>
                          <p class="col-3 text-right">2 hours</p>
                        </div>

                        <div class="row">
                          <div class="col-8">
                            <p class="card-subtitle">BIB 121</p>
                          </div>
                          <div class="col-4 text-right">
                            <span class="text-muted">Fall</span>
                          </div>
                        </div>
                        <div class="row">
                          <b-form-select
                            v-model="selected"
                            :options="options"
                          ></b-form-select>

                          <b-button
                            block
                            variant="outline-secondary"
                            class="my-2"
                            >Add</b-button
                          >
                        </div>

                        <div class="row">
                          <div class="col">
                            <a
                              href="#bib121"
                              class="card-link fw-light"
                              v-b-toggle="bib121"
                              >Course description ›</a
                            >
                          </div>
                        </div>

                        <b-collapse
                          class="course-description collapse card-text"
                          id="bib121"
                        >
                          <p class="text-muted card-text">
                            A thorough textual study of the life of Jesus the
                            Christ. Emphasis is given to his virgin birth, his
                            message and ministry, his crucifixion, his
                            resurrection, and his ascension, all leading to a
                            greater awareness of his greatness as the Son of God
                            and Savior of the world. Moral, doctrinal,
                            historical, and practical aspects of the life of
                            Christ are also emphasized. (Text course.)
                          </p>
                        </b-collapse>
                      </div>
                    </div> -->
                    <CourseInfo
                      v-for="l in lacCourses"
                      :key="l.id"
                      :course="l"
                      @add-course="addCourseToSchedule"
                    />
                  </div>
                </div>
              </b-tab>

              <b-tab title="CS">
                <div id="cs">
                  <div class="my-4 text-left" id="cs-reqs">
                    <!-- <div class="card my-2">
                      <div class="card-body">
                        <div class="row">
                          <h5 class="col-9">
                            <b>Computer Programming I</b>
                          </h5>
                          <p class="col-3 text-right">2 hours</p>
                        </div>

                        <div class="row">
                          <div class="col-8">
                            <p class="card-subtitle">BIB 121</p>
                          </div>
                          <div class="col-4 text-right">
                            <span class="text-muted">Fall</span>
                          </div>
                        </div>
                        <div class="row">
                          <div class="col">
                            <a
                              href="#bib121"
                              class="card-link fw-light"
                              v-b-toggle="bib121"
                              >Course description ›</a
                            >
                          </div>
                        </div>

                        <b-collapse
                          class="course-description collapse card-text"
                          id="bib121"
                        >
                          <p class="text-muted card-text">
                            A thorough textual study of the life of Jesus the
                            Christ. Emphasis is given to his virgin birth, his
                            message and ministry, his crucifixion, his
                            resurrection, and his ascension, all leading to a
                            greater awareness of his greatness as the Son of God
                            and Savior of the world. Moral, doctrinal,
                            historical, and practical aspects of the life of
                            Christ are also emphasized. (Text course.)
                          </p>
                        </b-collapse>
                      </div>
                    </div> -->
                    <CourseInfo
                      v-for="c in cssdCourses"
                      :key="c.id"
                      :course="c"
                      @add-course="addCourseToSchedule"
                    />
                  </div>
                </div>
              </b-tab>
            </b-tabs>
          </div>

          <!-- Semester Schedules -->
          <div class="col-lg-6 semester-schedules">
            <h3>Semester Schedules</h3>

            <!-- <div
              v-for="schedule in schedules"
              v-bind:key="schedule.id"
              class="accordion my-4"
              id="schedule.id"
            >
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
                      <tr>
                        <td>BIB 121</td>
                        <td>
                          <span class="fw-bold"> The Life of Christ </span>
                        </td>
                        <td>
                          <span class="badge bg-primary"> LAC </span>
                        </td>
                        <td>2</td>
                      </tr>
                      <tr>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td class="fw-bold">14</td>
                      </tr>
                    </table>
                  </div>
                </b-collapse>
              </div>
            </div> -->

            <SemesterSchedule
              v-for="s in schedules"
              :key="s.id"
              :schedule="s"
              :classes="s.classes"
              :id="s.id"
              class="accordion my-4"
            />
          </div>

          <!-- Table of Contents Sidebar -->
          <div class="col-lg-2 position-sticky top-0 h-100 ps-5 toc">
            <nav>
              <p class="text-muted">On this page</p>
              <ul>
                <li><a href="#fall2020">Fall 2020</a></li>
                <li><a href="#spring2021">Spring 2021</a></li>
                <li><a href="#fall2021">Fall 2021</a></li>
                <li><a href="#spring2022">Spring 2022</a></li>
                <li><a href="#fall2022">Fall 2022</a></li>
                <li><a href="#spring2023">Spring 2023</a></li>
                <li><a href="#fall2023">Fall 2023</a></li>
                <li><a href="#spring2024">Spring 2024</a></li>
              </ul>
            </nav>
          </div>
        </div>
      </div>
    </main>

    <!-- Footer -->
    <footer class="bg-dark text-light py-4">
      <div class="container-fluid">
        <div class="row">
          <div class="col">
            <p>Made with ❤️ by FHU students!</p>
          </div>

          <div class="col-md-3">
            <p>&copy; 2021 Freed-Hardeman University</p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import SemesterSchedule from "./components/SemesterSchedule.vue";
import CourseInfo from "./components/CourseInfo.vue";

export default {
  name: "App",
  components: {
    SemesterSchedule,
    CourseInfo,
  },
  data() {
    return {
      schedules: [
        {
          name: "Fall 2020",
          id: "fall2020",
          collapseId: "fall2019schedule",
          classes: [],
        },
        {
          name: "Spring 2021",
          id: "spring2021",
          collapseId: "spring2021schedule",
          classes: [],
        },
        {
          name: "Fall 2021",
          id: "fall2021",
          collapseId: "fall2021schedule",
          classes: [],
        },
        {
          name: "Spring 2022",
          id: "spring2022",
          collapseId: "spring2022schedule",
          classes: [],
        },
        {
          name: "Fall 2022",
          id: "fall2022",
          collapseId: "fall2022schedule",
          classes: [],
        },
        {
          name: "Spring 2023",
          id: "spring2023",
          collapseId: "spring2023schedule",
          classes: [],
        },
        {
          name: "Fall 2023",
          id: "fall2023",
          collapseId: "fall2023schedule",
          classes: [],
        },
        {
          name: "Spring 2024",
          id: "spring2024",
          collapseId: "spring2024schedule",
          classes: [],
        },
      ],
      allCourses: this.getAllCourses(), // json object
      lacCourses: [], // array of lac course objects
      cssdCourses: [], // array of cssd course objects
    };
  },
  methods: {
    getAllCourses() {
      var data = require("./courses.json");
      return data;
    },
    getLACCourses() {
      this.allCourses["LAC Courses"].forEach((course) => {
        this.lacCourses.push(course);
      });
    },
    getCSSDCourses() {
      this.allCourses["CSSD Courses"].forEach((course) => {
        this.cssdCourses.push(course);
      });
    },
    addCourseToSchedule(scheduleID, course) {
      // check if a semester is selected
      if (scheduleID == null) {
        console.log("No semester selected");
        return;
      }

      // add class to selected schedule
      this.schedules.forEach((s) => {
        if (s.id === scheduleID) {
          s.classes.push(course);
        }
      });

      console.log(`${course["Course ID"]} successfully added to ${scheduleID}`);
    },
  },
  mounted() {
    this.getLACCourses();
    this.getCSSDCourses();
  },
};
</script>

<style>
#app {
  font-family: "Nunito Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.toc nav {
  text-align: left;
}

.toc ul {
  padding: 0;
  list-style: none;
}

.toc li {
  margin: 0;
  margin-bottom: 0.5rem;
}

.toc li a {
  text-decoration: none;
}

.toc li a:hover {
  text-decoration: underline;
}

.required-classes .card {
  border-left: 8px solid #0c63e4;
}
</style>
