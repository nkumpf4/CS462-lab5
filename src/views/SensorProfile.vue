<template>
  <div class="flex flex-col items-center">
    <div class="p-8 bg-white rounded shadow w-96 mb-8">
      <h1 class="text-xl font-semibold mb-4">Current Sensor Profile</h1>
      <div>Location: {{ location }}</div>
      <div>Name: {{ name }}</div>
      <div>Threshold: {{ threshold }}</div>
      <div>Contact Number: {{ contactNumber }}</div>
    </div>
    <div class="p-8 bg-white rounded shadow w-96">
      <h1 class="text-xl font-semibold mb-4">Edit Sensor Profile</h1>
      <form class="flex flex-col" @submit.prevent="updateProfile()">
        <input
          type="text"
          placeholder="New Location"
          class="border bg-gray-50 p-2 mb-2 rounded"
        />
        <input
          type="text"
          placeholder="New Name"
          class="border bg-gray-50 p-2 mb-2 rounded"
        />
        <input
          type="number"
          placeholder="New Threshold"
          class="border bg-gray-50 p-2 mb-2 rounded"
        />
        <input
          type="text"
          placeholder="New Contact Number"
          class="border bg-gray-50 p-2 mb-2 rounded"
        />
        <input
          type="submit"
          class="rounded p-2 focus:outline-none bg-green-400 text-white active:bg-green-500 cursor-pointer"
          value="Save"
        />
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      location: "",
      name: "",
      threshold: null,
      contactNumber: ""
    };
  },
  methods: {
    getProfile() {
      console.log("Getting Profile");
    },
    updateProfile() {
      console.log("Updating Profile");
    }
  }
};
</script>
