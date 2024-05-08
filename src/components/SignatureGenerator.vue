<template>
  <div
    class="bg-white rounded-lg shadow-2xl sm:p-6 px-2 flex flex-col lg:flex-row sm:pt-6 pt-4"
  >
    <div class="lg:w-1/3 lg:pr-4 w-full">
      <InputField
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
    </div>
    <div
      class="lg:w-2/3 w-full lg:pl-4 pl-0 lg:border-l border-0 border-gray-300 flex justify-around items-center flex-col"
    >
      <div
        class="text-xl text-center text-[#ff0000] font-thin"
        :class="{
          'lg:-mt-8 sm:mt-8 my-8': isFormValid,
          'lg:-mt-14 sm:mt-8 mt-8': !isFormValid,
        }"
      >
        Preview
      </div>
      <div class="text-green-500 text-center h-4 my-6">
        <span v-if="showCopiedMessage">Signature copied!</span>
        <span
          v-else-if="
            !isFormValid && (name || jobTitle || phone || email || website)
          "
        >
          Please fill in all fields correctly to copy the signature.
        </span>
      </div>

      <div v-if="showSignaturePreview">
        <SignaturePreview
          :name="name"
          :jobTitle="jobTitle"
          :phone="formattedPhoneNumber"
          :email="email"
          :website="website"
          :companyLogo="showLogo ? companyLogo : null"
        />
      </div>

      <div class="flex items-center">
        <button
          v-if="inputFilled"
          @click="copySignature"
          :disabled="!isFormValid"
          class="bg-black hover:bg-[#FF0000] text-white py-2 px-4 rounded mx-auto transition-all delay-100 my-8 sm:mt-8"
          :class="{ 'opacity-50 cursor-not-allowed': !isFormValid }"
        >
          Copy Signature
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import InputField from "./InputField.vue";
import SignaturePreview from "./SignaturePreview.vue";
// import companyLogo from "../assets/logo.png";
// const companyLogo = "https://i.postimg.cc/vTYD6TzB/logo.png";
const companyLogo = "https://i.postimg.cc/vTYD6TzB/logo.png";

export default {
  components: {
    InputField,
    SignaturePreview,
  },
  setup() {
    const name = ref("");
    const jobTitle = ref("");
    const phone = ref("");
    const email = ref("");
    const website = ref("");
    const formattedPhoneNumber = ref("");
    const showCopiedMessage = ref(false);

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

    const inputFilled = computed(() => {
      return (
        name.value.trim() ||
        jobTitle.value.trim() ||
        phone.value.trim() ||
        email.value.trim() ||
        website.value.trim()
      );
    });

    const isFormValid = computed(() => {
      return (
        !jobTitleRules.some((rule) => rule(jobTitle.value) !== true) &&
        !phoneRules.some((rule) => rule(phone.value) !== true) &&
        !emailRules.some((rule) => rule(email.value) !== true) &&
        !websiteRules.some((rule) => rule(website.value) !== true)
      );
    });

    const showLogo = computed(() => {
      return (
        name.value.trim() ||
        jobTitle.value.trim() ||
        phone.value.trim() ||
        email.value.trim() ||
        website.value.trim()
      );
    });

    const showSignaturePreview = computed(() => {
      return (
        name.value ||
        jobTitle.value ||
        phone.value ||
        email.value ||
        website.value
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

    const copySignature = async () => {
      if (isFormValid.value) {
        const signatureContainer = document.querySelector(".signature-preview");
        const html = signatureContainer.outerHTML;
        await navigator.clipboard.writeText(html).then(() => {
          showCopiedMessage.value = true;
          setTimeout(() => {
            showCopiedMessage.value = false;
          }, 2000);
        });
      }
    };

    const handleInputChange = () => {
      showCopiedMessage.value = false;
    };

    return {
      name,
      jobTitle,
      phone,
      email,
      website,
      formattedPhoneNumber,
      showCopiedMessage,
      inputFilled,
      nameRules,
      jobTitleRules,
      phoneRules,
      emailRules,
      websiteRules,
      isFormValid,
      showLogo,
      showSignaturePreview,
      formatPhoneNumber,
      copySignature,
      handleInputChange,
      companyLogo,
    };
  },
};
</script>
