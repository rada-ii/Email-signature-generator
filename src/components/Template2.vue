<template>
  <div
    class="signature-preview"
    style="
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      width: 100%;
    "
  >
    <img
      v-if="companyLogo"
      :src="companyLogo"
      alt="Company Logo"
      class="img"
      style="width: 8rem; height: auto; margin-bottom: 1rem"
    />
    <div style="width: 100%; text-align: center">
      <div
        id="nameJobContainer"
        style="
          display: flex;
          flex-direction: column;
          align-items: center;
          text-align: center;
          margin-bottom: 0.5rem;
        "
      >
        <div style="font-weight: 400; font-size: 1.25rem; line-height: 1.4rem">
          {{ name }}
        </div>
        <div
          style="
            font-weight: 500;
            font-size: 1.25rem;
            line-height: 1.5rem;
            margin-top: 0.5rem;
          "
        >
          {{ jobTitle }}
        </div>
      </div>
      <div class="data-user" style="text-align: center; width: 100%">
        <div
          v-if="phone"
          class="phone"
          style="
            font-weight: 300;
            font-size: 1.125rem;
            line-height: 1rem;
            color: #000;
          "
        >
          <span style="font-weight: 300">phone:</span> {{ phone }}
        </div>
        <div
          v-if="email"
          class="email"
          style="font-weight: 300; font-size: 1.125rem; line-height: 1rem"
        >
          <span>email:</span>
          <a
            :href="`mailto:${email}`"
            style="color: #2563eb; text-decoration: underline"
          >
            {{ email }}
          </a>
        </div>
        <div
          v-if="website"
          class="site"
          style="font-weight: 300; font-size: 1.125rem; line-height: 0.7rem"
        >
          <span>website:</span>
          <a
            :href="`https://${website}`"
            target="_blank"
            style="color: #2563eb; text-decoration: underline"
          >
            {{ website }}
          </a>
        </div>
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
