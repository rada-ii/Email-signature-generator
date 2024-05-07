<template>
  <div class="mb-4">
    <label class="block lg:font-bold font-semibold mb-2" :for="label">{{
      label
    }}</label>
    <input
      :id="label"
      :value="modelValue"
      @input="handleInput"
      :placeholder="placeholder"
      class="w-full border border-gray-300 rounded py-2 px-4 focus:outline-none focus:ring-2 focus:ring-blue-500 cursor-pointer text-black"
    />
    <div v-if="errors.length" class="text-red-500 mt-1">
      <div v-for="error in errors" :key="error">
        <span>{{ error }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true,
    },
    modelValue: {
      type: String,
      required: true,
    },
    placeholder: {
      type: String,
      required: false,
    },
    rules: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      errors: [],
    };
  },
  methods: {
    handleInput(event) {
      const value = event.target.value;
      this.errors = [];
      let isValid = true;

      for (const rule of this.rules) {
        const result = rule(value);
        if (typeof result === "string") {
          this.errors.push(result);
          isValid = false;
        }
      }

      if (isValid) {
        this.$emit("update:modelValue", value);
      }
    },
  },
};
</script>
