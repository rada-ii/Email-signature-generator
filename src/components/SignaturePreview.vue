<template>
  <div
    class="signature-preview"
    style="display: flex; flex-direction: row; align-items: center"
  >
    <img
      v-if="companyLogo"
      :src="companyLogo"
      alt="Company Logo"
      style="
        width: 12.5rem;
        height: auto;
        margin-right: 1rem;
        padding-left: 0;
        padding-right: 1rem;
        border-right: 2px solid #ff0000;
      "
    />
    <div style="display: flex; flex-direction: column">
      <div
        id="nameJobContainer"
        style="display: flex; flex-direction: row; align-items: center"
      >
        <div
          style="
            font-weight: 400;
            font-size: 1.125rem;
            line-height: 1.2rem;
            margin-right: 1rem;
            padding-right: 1rem;
            border-right: 2px solid #d1d5db;
            text-transform: capitalize;
          "
        >
          {{ name }}
        </div>
        <div style="font-weight: 500; font-size: 1.125rem; line-height: 1rem">
          {{ jobTitle }}
        </div>
      </div>
      <div
        v-if="phone"
        style="
          font-weight: 300;
          font-size: 1.125rem;
          line-height: 1rem;
          color: #000;
        "
      >
        <span style="font-weight: 300">phone:</span>
        {{ phone }}
      </div>
      <div v-if="email">
        <span style="font-weight: 300; font-size: 1.125rem; line-height: 1rem"
          >email:</span
        >
        <a
          :href="`mailto:${email}`"
          style="
            color: #2563eb;
            text-decoration: underline;
            font-size: 1.125rem;
            line-height: 1rem;
          "
        >
          {{ email }}
        </a>
      </div>
      <div v-if="website" class="site">
        <span style="font-weight: 300; font-size: 1.125rem; line-height: 0.7rem"
          >website:</span
        >
        <a
          :href="`https://${website}`"
          target="_blank"
          style="
            color: #2563eb;
            text-decoration: underline;
            font-size: 1.125rem;
            line-height: 0.7rem;
          "
        >
          {{ website }}
        </a>
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
