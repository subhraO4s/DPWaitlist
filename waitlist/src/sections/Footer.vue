<template>
  <footer class="ftr">
    <h3 class="ftr-title">Follow Us For Exciting Updates</h3>
    <hr class="divider" />
    <ul class="socials">
      <li class="social-link"><a href="https://www.instagram.com/dezinepage/">Instagram</a></li>
      <li class="social-link"><a href="https://twitter.com/DezinePage/">Twitter</a></li>
      <li class="social-link">
        <a href="https://www.facebook.com/people/DezinePage/100092513988158/">Facebook</a>
      </li>
      <li class="social-link">
        <a href="https://www.linkedin.com/company/dezine-page/">Linkedin</a>
      </li>
    </ul>
  </footer>
</template>

<style scoped>
.ftr {
  width: 100%;
}

.ftr-title {
  font-weight: 500;
  font-size: 1rem;
  line-height: 24px;
  text-align: center;
  color: #667085;
}

.divider {
  width: 100%;
  border: 1px solid #323232;
}

.socials {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  padding-top: 0.25rem;
  padding-bottom: 0.25rem;
}

@media screen and (max-width: 800px) {
  .ftr {
    margin-top: 1rem;
  }
}

@media screen and (max-width: 550px) {
  .socials {
    justify-content: space-between;
  }
}
</style>
