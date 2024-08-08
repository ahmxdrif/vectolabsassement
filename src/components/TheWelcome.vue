<script setup>

</script>

<template>
  <div id="app">
<h1>Asset List</h1>
    <table border="1">
      <thead>
        <tr>
          <th>Asset Name</th>
          <th>Department</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(asset, index) in assets" :key="index">
          <td>{{ asset.name }}</td>
          <td>{{ asset.department }}</td>
        </tr>
      </tbody>
    </table>
    <button @click="downloadCSV">Download CSV</button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      assets: [
        { name: 'Printer', department: 'HR' },
        { name: 'Monitor', department: 'IT' },
        { name: 'Barcode Scanner', department: 'ACCOUNT' }
      ]
    };
  },
  methods: {
    downloadCSV() {
      const rows = [
        ['Asset Name', 'Department'],
        ...this.assets.map(asset => [asset.name, asset.department])
      ];
      let csvContent = "data:text/csv;charset=utf-8,"
        + rows.map(e => e.join(",")).join("\n");

      const link = document.createElement("a");
      link.setAttribute("href", encodeURI(csvContent));
      link.setAttribute("download", "assets.csv");
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }
};
</script>
<style>
#app {
  font-family: 'Montserrat', sans-serif;
  text-align: center;
  margin-top: 60px;
}
table {
  margin: 0 auto;
  border-collapse: collapse;
}

th, td {
  padding: 10px;
  text-align: left;
}
</style>