<template>
  <div class="section-3-wrapper">
    <h1 class="thankyou-text">Thank you</h1>
  </div>
</template>

<script>
  export default {
    name: "SectionThankYou",
  };
</script>

<style scoped>
    @font-face {
    font-family: "RecifeDisplay";
    src: url("@/assets/fonts/RecifeDisplay-BoldItalic.ttf") format("truetype");
    font-weight: 700;
    font-style: italic;
  }
  .section-3-wrapper {
    width: 100%;
    height: 100vh;
    background: #111606;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .thankyou-text {
    font-family: "RecifeDisplay", serif;
    font-size: 6rem;
    font-weight: 700;
    font-style: italic;
    color: #a8ff35;
    letter-spacing: 0.05em;
    line-height: 1;
    animation: fadeUp 1.2s ease-out forwards;
  }

  @keyframes fadeUp {
    from {
      opacity: 0;
      transform: translateY(40px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @media (max-width: 768px) {
    .thankyou-text {
      font-size: 3.5rem;
    }
  }

  @media (max-width: 480px) {
    .thankyou-text {
      font-size: 2.8rem;
    }
  }
</style>
