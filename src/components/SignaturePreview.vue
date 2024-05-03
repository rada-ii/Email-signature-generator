<template>
  <div class="flex items-center my-24 px-10">
    <img
      :src="companyLogo"
      alt="Company Logo"
      class="w-40 h-24 mr-4 pr-4 border-r border-[#FF0000]"
    />
    <div>
      <div class="flex justify-center">
        <div class="font-bold mr-4 pr-4 border-r border-gray-300">
          {{ name }}
        </div>
        <div>{{ jobTitle }}</div>
      </div>
      <div class="font-semibold text-red-500">{{ company }}</div>
      <div>
        email:<a :href="`mailto:${email}`" class="text-blue-500 hover:underline"
          >&nbsp;{{ email }}</a
        >
      </div>
      <div>
        website:
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
    company: {
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
};
</script>
