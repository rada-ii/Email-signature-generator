<template>
  <div
    class="signature-preview template-two"
    style="display: flex; flex-direction: column; align-items: center"
  >
    <img
      v-if="companyLogo"
      :src="companyLogo"
      alt="Company Logo"
      class="img"
      style="
        width: 12.5rem;
        height: auto;
        margin-right: 1rem;
        padding-left: 0;
        padding-right: 1rem;
        border-right: 2px solid #0000ff;
      "
    />
    <div style="display: flex; flex-direction: column">
      <div
        id="nameJobContainer"
        style="display: flex; flex-direction: row; align-items: center"
      >
        <div
          style="
            font-weight: 700;
            font-size: 1.125rem;
            line-height: 1.2rem;
            margin-right: 1rem;
            padding-right: 1rem;
            border-right: 2px solid #d1d5db;
            text-transform: uppercase;
          "
        >
          {{ name }}
        </div>
        <div
          style="
            font-weight: 700;
            font-size: 1.125rem;
            line-height: 1rem;
            text-transform: uppercase;
          "
        >
          {{ jobTitle }}
        </div>
      </div>
      <div class="data-user">
        <div
          class="phone"
          v-if="phone"
          style="
            font-weight: 500;
            font-size: 1.125rem;
            line-height: 1rem;
            color: #0000ff;
          "
        >
          <span style="font-weight: 500">phone:</span> {{ phone }}
        </div>
        <div v-if="email" class="email">
          <span style="font-weight: 500; font-size: 1.125rem; line-height: 1rem"
            >email:</span
          >
          <a
            :href="`mailto:${email}`"
            style="
              color: #0000ff;
              text-decoration: underline;
              font-size: 1.125rem;
              line-height: 1rem;
            "
            >{{ email }}</a
          >
        </div>
        <div v-if="website" class="site">
          <span
            style="font-weight: 500; font-size: 1.125rem; line-height: 0.7rem"
            >website:</span
          >
          <a
            :href="`https://${website}`"
            target="_blank"
            style="
              color: #0000ff;
              text-decoration: underline;
              font-size: 1.125rem;
              line-height: 0.7rem;
            "
            >{{ website }}</a
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["companyLogo", "name", "jobTitle", "phone", "email", "website"],
};
</script>
