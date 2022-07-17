<template>
  <div class="black-bg" v-if="isEditOpen == true">
    <div class="white-bg">
      <h4>QRT</h4>
      <p>대충 QRT 레포트 포맷 들어가는부분</p>
      <p>대충 QRT 레포트 포맷 들어가는부분</p>
      <p>대충 QRT 레포트 포맷 들어가는부분</p>
      <p>대충 QRT 레포트 포맷 들어가는부분</p>
      <p>대충 QRT 레포트 포맷 들어가는부분</p>
      <p>대충 QRT 레포트 포맷 들어가는부분</p>
      <button @click="isEditOpen = false">close</button>
    </div>
  </div>

  <div class="searchBar">
    <!-- Filter Search -->
    <div class="input-group mb-5">
      <input
        type="search"
        class="form-control"
        v-model="searchQuery"
        placeholder="Report Type"
        aria-label="Recipient's username"
        aria-describedby="button-addon2"
      />
    </div>
  </div>

  <table id="tableComponent" class="table table-bordered table-striped">
    <caption>
      Weathernews
    </caption>
    <thead>
      <tr>
        <!-- loop through each value of the fields to get the table header -->
        <th>QRT</th>
        <th v-for="field in fields" :key="field" @click="sortTable(field)">
          {{ field }}
          <i class="bi bi-sort-alpha-down" aria-label="Sort Icon"></i>
        </th>
      </tr>
    </thead>
    <tbody>
      <!-- Loop through the list get the each student data -->
      <tr v-for="item in filteredList" :key="item">
        <td test><button @click="isEditOpen = true">Edit</button></td>
        <td contenteditable v-for="field in fields" :key="field">
          {{ item[field] }}
        </td>
      </tr>
    </tbody>
  </table>
  <div></div>
</template>
<script>
import { computed, ref } from "vue";
// Importing  the lodash library
import { sortBy } from "lodash";

export default {
  name: "TableComponent",
  props: {
    studentData: {
      type: Array,
    },
    fields: {
      type: Array,
    },
  },
  data() {
    return {
      isEditOpen: false,
    };
  },
  setup(props) {
    let sort = ref(false);
    let updatedList = ref([]);
    let searchQuery = ref("");

    // a function to sort the table
    const sortTable = (col) => {
      sort.value = true;
      // Use of _.sortBy() method
      updatedList.value = sortBy(props.studentData, col);
    };

    const sortedList = computed(() => {
      if (sort.value) {
        return updatedList.value;
      } else {
        return props.studentData;
      }
    });

    // Filter Search
    const filteredList = computed(() => {
      return sortedList.value.filter((product) => {
        return (
          product.Report.toLowerCase().indexOf(
            searchQuery.value.toLowerCase()
          ) != -1
        );
      });
    });

    return { sortedList, sortTable, searchQuery, filteredList };
  },
};
</script>
<style scoped>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 90%;
  height: 90%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

table th:hover {
  background: #f2f2f2;
}
</style>