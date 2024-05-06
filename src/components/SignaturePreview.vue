<template class="">
  <div
    v-if="showLogo"
    ref="signatureContainer"
    class="flex items-center justify-center lg:mt-24 mt-12 mb-12 xl:px-10 px-0"
  >
    <img
      :src="companyLogo"
      alt="Company Logo"
      class="sm:w-40 w-24 h-28 lg:mr-4 sm:mr-4 mr-2 pl-0 sm:pr-4 pr-1 border-r border-[#FF0000] ml-0"
    />
    <div>
      <div class="flex flex-col xl:flex-row xl:items-center">
        <div
          class="sm:font-semibold font-normal sm:text-xl text-sm mr-4 pr-4 xl:border-r border-0 border-gray-300 text-transform: capitalize"
        >
          {{ name }}
        </div>
        <div class="font-semibold sm:text-xl text-sm">
          {{ jobTitle }}
        </div>
      </div>
      <div
        class="sm:font-semibold font-normal sm:text-xl text-sm text-[#ff0000]"
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
          class="text-blue-600 hover:underline transition-all delay-50 sm:font-semibold font-normal sm:text-xl text-sm"
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
          class="text-blue-600 hover:underline transition-all delay-50 sm:font-semibold font-normal sm:text-xl text-sm"
          >&nbsp;{{ website }}</a
        >
      </div>
    </div>
  </div>
  <div v-if="showLogo" class="flex items-center">
    <button
      @click="copySignature"
      class="bg-black hover:bg-[#FF0000] text-white py-2 px-4 rounded mx-auto transition-all delay-200 c"
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
  computed: {
    showLogo() {
      return (
        this.name || this.jobTitle || this.phone || this.email || this.website
      );
    },
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
