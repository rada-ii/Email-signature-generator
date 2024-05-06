<template>
  <div
    ref="signatureContainer"
    class="signature-preview flex items-center justify-center lg:mt-24 mt-12 mb-12 xl:px-10 px-0 leading-none"
  >
    <img
      :src="companyLogo"
      alt="Company Logo"
      class="sm:w-48 w-32 h-auto lg:mr-4 sm:mr-4 mr-2 pl-0 sm:pr-4 pr-1 border-r border-[#FF0000] ml-0"
    />
    <div class="datas">
      <div class="flex flex-col xl:flex-row xl:items-center">
        <div
          class="sm:font-normal font-normal sm:text-lg lg:text-base text-xs mr-4 pr-4 xl:border-r border-0 border-gray-300 text-transform: capitalize"
        >
          {{ name }}
        </div>
        <div class="font-normal sm:text-lg lg:text-base text-xs sm:pb-0 pb-1">
          {{ jobTitle }}
        </div>
      </div>
      <div
        class="sm:font-normal font-light sm:text-lg lg:text-base text-xs text-[#ff0000]"
      >
        <span v-if="phone" class="text-black sm:font-normal font-light"
          >phone:</span
        >
        {{ phone }}
      </div>
      <div>
        <span
          v-if="email"
          class="sm:font-normal font-light sm:text-lg lg:text-base text-xs"
          >email:</span
        >
        <a
          :href="`mailto:${email}`"
          class="text-blue-600 hover:underline transition-all delay-50 sm:font-normal font-light sm:text-xl lg:text-base text-xs"
          >&nbsp;{{ email }}</a
        >
      </div>
      <div>
        <span
          v-if="website"
          class="sm:font-normal font-light sm:text-lg lg:text-base text-xs"
          >website:</span
        >
        <a
          :href="`https://${website}`"
          target="_blank"
          class="text-blue-600 hover:underline transition-all delay-50 sm:font-normal font-normal sm:text-lg lg:text-base text-xs"
          >&nbsp;{{ website }}</a
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    jobTitle: String,
    phone: String,
    email: String,
    website: String,
    companyLogo: String,
  },
};
</script>

<!-- <style scoped>
.signature-preview * {
  line-height: 1;
}
</style> -->
