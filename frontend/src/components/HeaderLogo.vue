<template>
    <div>
        <nav>
            <router-link to = "/">
                <i class="fas fa-arrow-left" id="home_arrow" @click="logUserOut()" ></i>
            </router-link>
            <div class = "signup_page_img">
                <img id = "black-logo" alt="groupomania logo" src="../assets/icon-left-font-monochrome-black.svg" />
            </div> 
        </nav>
    </div>
</template>

<script>
export default {
  data() {
    return {
      user: {}
    };
  },
  methods: {
      logUserOut() {
      localStorage.removeItem("user");
      this.$router.push("/");
    }
  }
}

</script>



<style>

nav {
    display: flex;
    margin: 1rem;
}

i {
    font-size: 1.5rem;
    padding: .5rem;
    color: black;
    margin: 1.75rem 0 0 1.5rem;
}

#black-logo {
    margin: 1rem 0 0 3rem;
    padding: 0;
    width: auto;
    height: 4rem;
}

@media screen and (max-width: 768px) {
    #black-logo {
        width: 50vw;
        margin: 1rem 0 0 1rem;
    }
}
</style>