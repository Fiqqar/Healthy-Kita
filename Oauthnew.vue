
<script>
import Cookies from 'js-cookie'
import { onMounted } from 'vue';
import { useRoute } from 'vue-router';

export default {
  name: 'oauthGoogle',

  setup() {
    const route = useRoute();  

    onMounted(() => {
      const encKey = route.query.encKey;
      const ivKey = route.query.ivKey;
      const accessToken = route.query.accessToken;
      const email = route.query.email



      if (accessToken) {
        localStorage.setItem("oauth", accessToken);
        Cookies.set('tokenUser', email, { expires: 3500, path: '/' });
      }

      if (encKey && ivKey) {
    
    //please store this at indexedDb of encKey and ivKey
      } else {
        console.log('encKey or ivKey is missing.');
      }

      window.location.href = `http://localhost:8080/home`
    });
    
  },
};
</script>

<style scoped>
</style>
