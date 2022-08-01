<template>
  <div class="copyright">
    <p>
      This game owned by Nam Hoai in Vue 3 course for begginers -
      <a href="https://github.com/hoainam2827" target="blank">view here</a>
    </p>
  </div>
</template>

<script>
export default {};
</script>

<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}
.copyright a {
  color: #f4dc26;
}</style>
