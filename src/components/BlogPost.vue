<script setup>
    const props=defineProps({
        id:Number,
        title:String,
        body:String
    })
</script>
<template>
    <div class="card">
        <ul>
            <li>{{ id }}</li>
            <li class="card-title">{{ title }}</li>
            <li  class="card-text">{{ body }}</li>
        </ul>
    </div>
</template>