<script>
  import { link } from "svelte-routing";
</script>

<style>
  footer {
    position: absolute;
    bottom: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    height: 3rem;
    z-index: -1;
    background-color: var(--red-2);
  }

  .logo-container {
    display: flex;
    align-items: center;
    margin-right: 1rem;
  }

  span {
    color: var(--white);
    margin-left: 1rem;
  }

  .logo-desc {
    display: none;
  }

  .logo-background {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 35px;
    height: 35px;
    border-radius: 17px;
    background-color: var(--white);
  }

  img {
    position: relative;
    width: 25px;
    height: auto;
  }
</style>

<footer>
  <span>&copy Manuel Proß</span>
  <div class="logo-container">
    <span class="logo-desc">Built with</span>
    <div class="logo-background">
      <img src="../images/Svelte_Logo.png" alt="Svelte Logo" />
    </div>
  </div>
</footer>
