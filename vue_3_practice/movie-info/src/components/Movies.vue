<template >
    <h1>영화 정보</h1>
    <div v-for="(item) in data" :key="item.id">
        <div class="item">
        <figure>
            <img :src="`${item.imageUrl}`" :alt="item.title"/>
        </figure>
        <div class="info">
            <h3>{{ item.title }}</h3>
            <p>개봉: {{ item.year }}</p>
            <p>장르: {{ item.category }}</p>
            <button @:click="$emit('increaseLike', item.id)">좋아요</button>
            <span>{{item.like}}</span>
            <p>
            <button @:click="$emit('openModal', item.id);">상세보기</button>
            </p>
        </div>
        </div>
    </div>
</template>
<script>
    export default {
        name: "MoviesComponent",
        props:{
            data: Array
        }
    }
</script>
<style>
    
</style>