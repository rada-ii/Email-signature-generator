<template>
  <div>
    <div class="radio-buttons text-center pb-8">
      <input
        type="radio"
        id="template1"
        value="template1"
        v-model="selectedTemplate"
        name="template"
      />
      <label for="template1" class="pr-4">&nbsp;Template 1</label>
      <input
        type="radio"
        id="template2"
        value="template2"
        v-model="selectedTemplate"
        name="template"
      />
      <label for="template2">&nbsp;Template 2</label>
    </div>

    <div class="bg-white rounded-lg shadow-2xl p-2 flex flex-col lg:flex-row">
      <div class="w-full lg:w-1/3 pr-4">
        <InputField
          class="pt-4"
          v-model="name"
          label="Name"
          placeholder="Enter your name"
          :rules="nameRules"
          @input="handleInputChange"
        />
        <InputField
          v-model="jobTitle"
          label="Job Title"
          placeholder="Enter your job title"
          :rules="jobTitleRules"
          @input="handleInputChange"
        />
        <InputField
          v-model="phone"
          label="Phone"
          placeholder="Enter your phone number"
          :rules="phoneRules"
          @input="formatPhoneNumber"
        />
        <InputField
          v-model="email"
          label="Email"
          placeholder="Enter your email address"
          :rules="emailRules"
          @input="handleInputChange"
        />
        <InputField
          v-model="website"
          label="Website"
          placeholder="Enter your website URL"
          :rules="websiteRules"
          @input="handleInputChange"
        />
        <input
          type="file"
          @change="handleLogoUpload"
          accept="image/*"
          class="pb-4"
        />
      </div>

      <div
        class="w-full lg:w-2/3 lg:border-l border-gray-300 flex flex-col items-center justify-center"
      >
        <div class="text-xl text-center text-[#ff0000] font-thin my-8">
          Preview
        </div>
        <SignaturePreview
          ref="signaturePreview"
          :key="`${name}-${jobTitle}-${phone}-${email}-${website}-${companyLogo}-${selectedTemplate}`"
          :name="name"
          :jobTitle="jobTitle"
          :phone="formattedPhoneNumber"
          :email="email"
          :website="website"
          :companyLogo="companyLogo"
          :templateType="selectedTemplate"
        />

        <button
          v-if="hasStartedTyping"
          @click="copySignature"
          :disabled="!isFormValid"
          class="bg-black hover:bg-[#FF0000] text-white py-2 px-4 rounded mx-auto transition-all delay-100 my-8 sm:mt-8"
          :class="{ 'opacity-50 cursor-not-allowed': !isFormValid }"
        >
          Copy Signature
        </button>

        <div class="text-green-500 text-center h-4 my-2">
          <span v-if="showCopiedMessage">Signature copied!</span>
          <span v-else-if="!isFormValid">
            Please fill in all fields correctly to copy the signature.
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import InputField from "./InputField.vue";
import SignaturePreview from "./SignaturePreview.vue";

export default {
  components: {
    InputField,
    SignaturePreview,
  },
  setup() {
    const hasStartedTyping = ref(false);

    const handleInputChange = () => {
      showCopiedMessage.value = false;
      hasStartedTyping.value = true;
      isFormValid.value = isFormValid.value;
    };
    const selectedTemplate = ref("template1");
    const name = ref("");
    const jobTitle = ref("");
    const phone = ref("");
    const email = ref("");
    const website = ref("");
    const formattedPhoneNumber = ref("");
    const showCopiedMessage = ref(false);
    const companyLogo = ref(null);
    const signaturePreview = ref(null);

    const nameRules = [
      (v) =>
        /^[a-zA-ZčćšđžČĆŠĐŽ'\s]+$/.test(v) ||
        "Name should contain only letters, accents, and spaces",
    ];

    const jobTitleRules = [
      (v) =>
        /^[a-zA-Z\s]+$/.test(v) ||
        "Job title should contain only letters and spaces",
    ];

    const phoneRules = [
      (v) => !!v || "Phone number is required",
      (v) =>
        /^[\d\s]+$/.test(v) ||
        "Phone number must contain only digits and spaces",
    ];

    const emailRules = [
      (v) => !!v || "Email is required",
      (v) =>
        /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) ||
        "Invalid email address",
    ];

    const websiteRules = [
      (v) => !!v || "Website is required",
      (v) =>
        /^(https?:\/\/)?[\w.-]+\.[a-zA-Z]{2,}$/.test(v) ||
        "Invalid website URL",
    ];
    const isFormValid = computed(() => {
      const validName = nameRules.every((rule) => rule(name.value) === true);
      const validJobTitle = jobTitleRules.every(
        (rule) => rule(jobTitle.value) === true
      );
      const validPhone = phoneRules.every((rule) => rule(phone.value) === true);
      const validEmail = emailRules.every((rule) => rule(email.value) === true);
      const validWebsite = websiteRules.every(
        (rule) => rule(website.value) === true
      );

      return (
        validName && validJobTitle && validPhone && validEmail && validWebsite
      );
    });

    const formatPhoneNumber = () => {
      let phoneValue = phone.value.replace(/\s/g, "");
      if (phoneValue.startsWith("0")) {
        phoneValue = phoneValue.substring(1);
      }
      const formattedValue = phoneValue.replace(
        /(\d{3})(\d{3})(\d*)/,
        "$1 $2 $3"
      );
      formattedPhoneNumber.value = formattedValue;
    };

    const handleLogoUpload = (event) => {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          companyLogo.value = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    };

    const copySignature = () => {
      if (isFormValid.value) {
        const signatureContainer = signaturePreview.value.$el;
        const html = signatureContainer.outerHTML;
        navigator.clipboard
          .writeText(html)
          .then(() => {
            showCopiedMessage.value = true;
            setTimeout(() => {
              showCopiedMessage.value = false;
            }, 2000);
          })
          .catch((err) => {
            console.error("Failed to copy signature: ", err);
          });
      }
    };

    return {
      name,
      jobTitle,
      phone,
      email,
      website,
      formattedPhoneNumber,
      showCopiedMessage,
      nameRules,
      jobTitleRules,
      phoneRules,
      emailRules,
      websiteRules,
      isFormValid,
      formatPhoneNumber,
      handleLogoUpload,
      companyLogo,
      selectedTemplate,
      signaturePreview,
      copySignature,
      hasStartedTyping,
      handleInputChange,
    };
  },
};
</script>
