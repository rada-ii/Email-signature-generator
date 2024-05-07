<template>
  <div
    class="container mx-auto flex flex-col justify-center min-h-screen sm:p-8 px-2 w-full"
  >
    <h1
      class="sm:text-2xl text-xl lg:font-semibold my-4 text-center text- font-thin text-black"
    >
      Daxon <span class="text-[#FF0000]">Email Signature</span> Generator
    </h1>
    <SignatureGenerator />
  </div>
</template>

<script>
import SignatureGenerator from "./components/SignatureGenerator.vue";

export default {
  components: {
    SignatureGenerator,
  },
};
</script>
