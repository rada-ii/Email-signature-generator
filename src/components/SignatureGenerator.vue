<template>
  <div class="bg-white rounded-lg shadow-2xl p-6 flex flex-col lg:flex-row">
    <div class="lg:w-1/2 lg:pr-4 pb-6 w-full">
      <InputField
        v-model="state.name"
        label="Name"
        placeholder="Enter your name"
      />
      <InputField
        v-model="state.jobTitle"
        label="Job Title"
        placeholder="Enter your job title"
      />
      <InputField
        v-model="state.phone"
        label="Phone"
        placeholder="Enter your phone number"
      />
      <InputField
        v-model="state.email"
        label="Email"
        placeholder="Enter your email address"
      />
      <InputField
        v-model="state.website"
        label="Website"
        placeholder="Enter your website URL"
      />
    </div>
    <div
      class="lg:w-1/2 w-full lg:pl-4 pl-0 lg:border-l border-0 border-gray-300"
    >
      <div class="my-4 font-bold text-lg text-center text-[#ff00007e]">
        Preview
      </div>
      <SignaturePreview
        :name="state.name"
        :jobTitle="state.jobTitle"
        :phone="state.phone"
        :email="state.email"
        :website="state.website"
        :companyLogo="companyLogo"
        :showLogo="showLogo"
      />
    </div>
  </div>
</template>

<script>
import { reactive, computed } from "vue";
import InputField from "./InputField.vue";
import SignaturePreview from "./SignaturePreview.vue";
import companyLogo from "../assets/logo.png";

export default {
  components: {
    InputField,
    SignaturePreview,
  },
  setup() {
    const state = reactive({
      name: "",
      jobTitle: "",
      phone: "",
      email: "",
      website: "",
    });

    const showLogo = computed(() => {
      return (
        state.name ||
        state.jobTitle ||
        state.phone ||
        state.email ||
        state.website
      );
    });

    return {
      state,
      companyLogo,
      showLogo,
    };
  },
};
</script>
