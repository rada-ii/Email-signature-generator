<template>
  <div
    v-if="showLogo"
    ref="signatureContainer"
    class="flex items-center justify-center mt-24 mb-12 xl:px-10 px-0"
  >
    <img
      :src="companyLogo"
      alt="Company Logo"
      class="sm:w-40 w-20 h-24 lg:mr-4 sm:mr-4 mr-2 lg:p-4 pl-0 sm:pr-4 pr-1 border-r border-[#FF0000] ml-0"
    />
    <div>
      <div class="flex flex-col xl:flex-row xl:items-center gap-5 pb-4">
        <div
          class="sm:font-semibold font-normal sm:text-xl text-sm mr-4 pr-4 xl:border-r border-0 border-gray-300 text-transform: capitalize"
        >
          {{ name }}
        </div>
        <div class="sm:font-semibold font-normal sm:text-xl text-sm">
          {{ jobTitle }}
        </div>
      </div>
      <div
        class="sm:font-semibold font-normal sm:text-xl text-sm text-red-500 pb-4"
      >
        <span v-if="phone" class="text-black">phone:</span> {{ phone }}
      </div>
      <div>
        <span
          v-if="email"
          class="sm:font-semibold font-normal sm:text-xl text-sm"
          >email:</span
        >
        <a
          :href="`mailto:${email}`"
          class="text-blue-500 hover:underline sm:font-semibold font-normal sm:text-xl text-sm"
          >&nbsp;{{ email }}</a
        >
      </div>
      <div>
        <span
          v-if="website"
          class="sm:font-semibold font-normal sm:text-xl text-sm"
          >website:</span
        >
        <a
          :href="`https://${website}`"
          target="_blank"
          class="text-blue-500 hover:underline sm:font-semibold font-normal sm:text-xl text-sm"
          >&nbsp;{{ website }}</a
        >
      </div>
    </div>
  </div>
  <div class="flex items-center">
    <button
      @click="copySignature"
      class="mt-4 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mx-auto"
    >
      Copy Signature
    </button>
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
    showLogo: Boolean,
  },
  methods: {
    copySignature() {
      const el = this.$refs.signatureContainer;
      const range = document.createRange();
      const selection = window.getSelection();
      range.selectNodeContents(el);
      selection.removeAllRanges();
      selection.addRange(range);
      document.execCommand("copy");
      alert("Signature copied!");
      selection.removeAllRanges();
    },
  },
};
</script>
