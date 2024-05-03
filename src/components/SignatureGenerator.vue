<template>
  <div class="bg-white rounded-lg shadow-2xl p-6 flex">
    <div class="w-1/2 pr-4">
      <InputField v-model="name" label="Name" placeholder="Enter your name" />
      <InputField
        v-model="jobTitle"
        label="Job Title"
        placeholder="Enter your job title"
      />
      <InputField
        v-model="company"
        label="Company"
        placeholder="Enter your company name"
      />
      <InputField
        v-model="email"
        label="Email"
        placeholder="Enter your email address"
      />
      <InputField
        v-model="website"
        label="Website"
        placeholder="Enter your website URL"
      />
    </div>
    <div class="w-1/2 pl-4 border-l border-gray-300">
      <div class="mb-4 font-bold text-lg text-center">Preview</div>
      <SignaturePreview
        :name="name"
        :jobTitle="jobTitle"
        :company="company"
        :email="email"
        :website="website"
        :companyLogo="companyLogo"
      />
    </div>
  </div>
</template>

<script>
import InputField from "./InputField.vue";
import SignaturePreview from "./SignaturePreview.vue";
import companyLogo from "../assets/logo.png";

export default {
  components: {
    InputField,
    SignaturePreview,
  },
  data() {
    return {
      name: "",
      jobTitle: "",
      company: "",
      email: "",
      website: "",
      companyLogo: companyLogo,
    };
  },
};
</script>
