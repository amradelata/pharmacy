<template>
  <div dir="rtl" lang="ar">
    <myVav />
    <notification />
    <div class="map">
      <iframe
        src="https://www.google.com/maps/embed?pb=!1m14!1m12!1m3!1d13913.965682582799!2d30.86137795!3d29.326590599999996!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!5e0!3m2!1sen!2seg!4v1580298588986!5m2!1sen!2seg"
        width="100%"
        height="100%"
        frameborder="0"
        style="border:0;"
        allowfullscreen
      ></iframe>
    </div>
  </div>
</template>

<script>
import myVav from "~/components/myVav.vue";
import notification from "~/components/notification.vue";

export default {
  components: {
    myVav,
    notification
  }
};
</script>


<style>
</style>