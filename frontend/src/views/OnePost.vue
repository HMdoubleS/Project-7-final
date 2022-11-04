<template>
    <HeaderLogo />
    <RouterLink to="/home">
        <button class="btn btn-primary btn-med" id="home_btn" role="button"><strong>Home</strong></button>
    </RouterLink>
    <OnePost />
    <RouterView />
</template>

<script>
import HeaderLogo from '@/components/HeaderLogo.vue';
import OnePost from '@/components/OnePost.vue';

export default {
    data() {
      return {
        posts: []
      }
    },
        
    components: {
      HeaderLogo,
      OnePost
    }
}

</script>



<style scoped>
#home_btn {
  margin: 2rem 0 4rem 8rem;
  font-size: 18px;
}

@media screen and (max-width: 768px) {
  #home_btn {
    margin: 1rem 0 2rem 3rem;
    font-size: 18px;
  }
}
</style>