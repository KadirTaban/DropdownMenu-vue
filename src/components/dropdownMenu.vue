<template> 
    <section class="dropdown-wrapper">
        <div class="selected-item">
            <span>Select User </span>
        </div>
        <div class="dropdown-popover">
            <input v-model="searchQuery" type = "text" placeholder="Search for User">
            <div class="options">
                <ul>
                    <li>Kadir</li>
                    <li>Alper</li>
                    <li>Berat</li>
                    <li>Erol</li>
                    <li>Şavşat</li>
                </ul>
            </div>
        </div>
    </section>
</template>

<script>
export default{};
</script>


<style scoped lang="scss"> 
.dropdown-wrapper {
    max-width: 350px;
    position: relative;
    margin: 0 auto;

}
.selected-item {
    height: 40px;
    border: 2px solid lightgray;
    border-radius: 5px;
    padding: 5px 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size:10px;
    font-weight: medium;
    
}
.dropdown-popover{
    position: absolute;
    border:2px;
    top:40px;
    left:0;
    right:0;
    background-color: #fff;
    width:100%;
    padding: 10px;
}
.options{
    width: 100%;
    ul{
        list-style: none;
        text-align: left;
        padding-left: 8px;
        max-height: 200px ;
        overflow-y:scroll;
        overflow-x: hidden;
        
    
    li{
        width:100%;
        border-bottom:1px solid lightgray;
        padding:10px;


    }
    }
}


</style>