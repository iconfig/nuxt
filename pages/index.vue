<template>
<div>
    关于
     <ul>
         <li v-for="(item,index) in list" :key="index">{{item.name}}</li>
     </ul>
</div>
</template>

<script lang="ts" setup>
let {data:list} = await useFetch('/api/channel')
</script>

<style>

</style>