<template>
  <GeneralUse :type="$route.params.type" navbar="true" breadcrumb_detail="true" bookform="true" gameform="true" giftform="true" materialform="ture"/>

</template>

<script>
// @ is an alias to /src
import GeneralUse from "@/components/GeneralUse.vue";
export default {
  name: "DetailView",
  components: {
    GeneralUse,
  },
};
</script>
