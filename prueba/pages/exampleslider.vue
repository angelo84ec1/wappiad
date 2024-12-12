<!-- pages/index.vue o cualquier otro componente -->
<template>
  <div>
    <SubMenu title="Menú Principal" />
  </div>
</template>

<script setup>
import SubMenu from '~/components/SubMenu.vue';


const isActive = ref(false);
const showSubMenu = reactive({
  asistencias: false,
});

const toggleSubMenu = (menuItem) => {
  showSubMenu[menuItem] = !showSubMenu[menuItem];
};

const closeSubMenu = () => {
  showSubMenu.asistencias = false;
};
</script>

<script>
export default {
  components: {
    SubMenu,
  },
  setup() {
    return {
      isActive,
      showSubMenu,
      toggleSubMenu,
      closeSubMenu,
    };
  },
};
</script>

