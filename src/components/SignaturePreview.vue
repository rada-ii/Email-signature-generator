<template>
  <div v-if="showLogo" class="flex items-center my-24 px-10">
    <img
      :src="companyLogo"
      alt="Company Logo"
      class="w-40 h-24 mr-4 pr-4 border-r border-[#FF0000]"
    />
    <div>
      <div class="flex">
        <div
          class="font-bold mr-4 pr-4 border-r border-gray-300 text-transform: capitalize"
        >
          {{ name }}
        </div>
        <div>{{ jobTitle }}</div>
      </div>
      <div class="font-semibold text-red-500 text-transform: capitalize">
        <span v-if="phone" class="text-black">phone:</span> {{ phone }}
      </div>
      <div>
        <span v-if="email">email:</span>
        <a :href="`mailto:${email}`" class="text-blue-500 hover:underline"
          >&nbsp;{{ email }}</a
        >
      </div>
      <div>
        <span v-if="website">website:</span>
        <a
          :href="`https://${website}`"
          target="_blank"
          class="text-blue-500 hover:underline"
          >&nbsp;{{ website }}</a
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true,
    },
    jobTitle: {
      type: String,
      required: true,
    },
    phone: {
      type: String,
      required: true,
    },
    email: {
      type: String,
      required: true,
    },
    website: {
      type: String,
      required: true,
    },
    companyLogo: {
      type: String,
      required: true,
    },
  },
  computed: {
    showLogo() {
      return (
        this.name || this.jobTitle || this.phone || this.email || this.website
      );
    },
  },
};
</script>
