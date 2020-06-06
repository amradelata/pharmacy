<template></template>

<script>
export default {
  mounted: function() {
    if (navigator.geolocation) {
      var self = this;
      navigator.geolocation.getCurrentPosition(function(position) {
        self.position = position;
        // self.position = position.coords.latitude;
      });
    }
    console.log(self);
  }
};
</script>