<template>
  <div class="flex flex-col items-center">
    <div class="p-8 mb-8 bg-white rounded shadow w-96">
      <h1 class="mb-4 text-xl font-semibold">Current Sensor Profile</h1>
      <div>Name: {{ name }}</div>
      <div>Location: {{ location }}</div>
      <div>Threshold: {{ threshold }}</div>
      <div>Contact Number: {{ contactNumber }}</div>
    </div>
    <div class="p-8 bg-white rounded shadow w-96">
      <h1 class="mb-4 text-xl font-semibold">Edit Sensor Profile</h1>
      <form class="flex flex-col" @submit.prevent="updateProfile()">
        <input
          type="text"
          placeholder="New Name"
          class="p-2 mb-2 border rounded bg-gray-50"
          v-model="newName"
        />
        <input
          type="text"
          placeholder="New Location"
          class="p-2 mb-2 border rounded bg-gray-50"
          v-model="newLocation"
        />
        <input
          type="number"
          placeholder="New Threshold"
          class="p-2 mb-2 border rounded bg-gray-50"
          v-model.number="newThreshold"
        />
        <input
          type="text"
          placeholder="New Contact Number"
          class="p-2 mb-2 border rounded bg-gray-50"
          v-model="newContactNumber"
        />
        <input
          type="submit"
          class="p-2 text-white bg-green-400 rounded cursor-pointer focus:outline-none active:bg-green-500"
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
      name: "",
      location: "",
      threshold: null,
      contactNumber: "",
      newName: "",
      newLocation: "",
      newThreshold: null,
      newContactNumber: ""
    };
  },
  mounted() {
    this.getProfile();
  },
  methods: {
    getProfile() {
      fetch(
        "http://192.168.11.11:3000/sky/cloud/ckkuoyesy00fawbu804nkd1eo/sensor_profile/profile"
      )
        .then(response => (this.log = response.json()))
        .then(json => {
          this.name = json.name;
          this.location = json.location;
          this.threshold = json.threshold;
          this.contactNumber = json.contact_number;
        });
    },
    updateProfile() {
      console.log("Updating");
      fetch(
        `http://192.168.11.11:3000/sky/event/ckkuoyesy00fawbu804nkd1eo/temp/profile/updated?name=${this.newName}&location=${this.newLocation}&threshold=${this.newThreshold}&contact_number=%2B1${this.newContactNumber}`,
        { method: "POST" }
      )
        .then(response => (this.log = response.json()))
        .then(json => console.log(json))
        .then(this.getProfile());
    }
  }
};
</script>
