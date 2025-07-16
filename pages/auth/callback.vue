<template>
  <div class="p-4">signing you in ...</div>
</template>
<script>
export default {
  async mounted() {
    try {
      await this.$auth.fetchUser();
      this.$router.replace("/");
    } catch (error) {
      console.error("login failed:",error);
      this.$router.push("/auth/signin");
    }
  },
};
</script>
