<script setup>
import { donors } from './donors/data/donorslist';

// Filter only A+ donors
const aPlusDonors = donors.filter(d => d.b_group === "A+");

// Count available donors
const availableCount = aPlusDonors.filter(d => d.available).length;

// HTML message
const htmlMessage = "<strong>Note:</strong> Please contact donors before visiting.";
</script>

<template>
  <div>
    <!-- Image via CDN -->
    <img src="https://via.placeholder.com/150" alt="Donor Image" />

    <h2>A+ Donors</h2>
    <p>Total Available Donors: {{ availableCount }}</p>

    <table border="1" cellpadding="6">
      <thead>
        <tr>
          <th>Ser</th>
          <th>Name</th>
          <th>Blood Group</th>
          <th>City</th>
          <th>Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(donor, index) in aPlusDonors" :key="donor.id">
          <td>{{ index + 1 }}</td>
          <td>{{ donor.name }}</td>
          <td>{{ donor.b_group }}</td>
          <td>{{ donor.city.toUpperCase() }}</td>
          <!-- v-show example: only show "Available" if donor.available -->
          <td v-html="donor.available
          ? '<span class=\'green\'>Available</span>' 
          : '<span class=\'red\'>Not Available</span>'">

          </td>
        </tr>
      </tbody>
    </table>

    <!-- v-html example -->
    <div v-html="htmlMessage" style="margin-top:10px;"></div>
  </div>
</template>

<style scoped>
table {
  border-collapse: collapse;
  width: 100%;
  margin-top: 10px;
}
th, td {
  border: 1px solid #000;
  text-align: left;
}
img {
  display: block;
  margin-bottom: 10px;
}
.green{
    color: green;
    font-weight: bold;
}
.red{
    color:red;
}
</style>
