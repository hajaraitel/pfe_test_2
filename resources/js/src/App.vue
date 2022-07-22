<template>
  <component :is="resolveLayout">
    <router-view></router-view>
  </component>
</template>

<script>
import { computed } from '@vue/composition-api'
import { useRouter } from '@/utils'
import LayoutBlank from '@/layouts/Blank.vue'
import LayoutContent from '@/layouts/Content.vue'
import userContent from '@/layouts/userContent.vue'
import adminContent from '@/layouts/adminContent.vue'

export default {
  components: {
    LayoutBlank,
    LayoutContent,userContent,adminContent
  },
  setup() {
    const { route } = useRouter()

    const resolveLayout = computed(() => {
      console.log(route.value.name);
      // Handles initial route

      if (route.value.name === null) return null

      if(route.value.name === 'userdashboard') return 'user-content'

      if(route.value.name === 'admindashboard') return 'admin-content'

      if (route.value.meta.layout === 'blank') return 'layout-blank'

      return 'layout-content'
    })

    return {
      resolveLayout,
    }
  },
}
</script>
