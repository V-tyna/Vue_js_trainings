<script setup>
  defineProps(['title', 'description']);
 </script>
 
 <template>
 <h4>
   {{ title }}
  </h4>
   <span>Decription: {{ description }} </span>
 </template>