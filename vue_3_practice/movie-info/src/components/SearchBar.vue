<template>
    <div class="search-box">
        <input placeholder="검색어 입력" type="search" @change="$emit('searchMovie', $event.target.value); inputText = $event.target.value; $event.target.value = ''">
        <button>검색</button>
    </div>
    <p>{{inputText}}</p>
</template>
<script>
export default {
    name: "SearchBarComponent",
    data(){
        return{
            inputText: "",
        }
    },
    watch:{
        inputText(name){
            const findName = this.data.filter(movie => {
                return movie.title.includes(name);
            });
            if(findName.length == 0){
                alert('해당하는 자료가 없습니다');
            }
        }
    },
    props:{
        data: Array
    }
}
</script>
<style>
    .search-box{
        padding: 10px;
        display: flex;
        justify-content: center;
    }
    .search-box input{
        padding: 5px 10px;
    }
    .search-box button{
        margin: 0;
    }
</style>