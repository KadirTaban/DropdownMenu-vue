<template> 
    <section class="dropdown-wrapper">
        <svg @click="isVisible = !isVisible" class="selected-item">
            <span>Select User </span>
            <svg 
            class="dropdown-icon"
            xmlns="http://www.w3.org/2000/svg" 
            viewBox="0 0 24 24" width="24"
            height="24"
            >
            <path fill="none" d="M0 0h24v24H0z"/>
            <path d="M3 4h18v2H3V4zm0 7h18v2H3v-2zm0 7h18v2H3v-2z"/></svg>
            
        </svg>
        <div v-if="isVisible" class="dropdown-popover">
            <div class="options">
                <ul>
                    <li>
                        <label for="toggle_button" >
                        <span v-if="isActive" class="toggle__label">On</span>
                        <span v-if="! isActive" class = "toggle__label">Off</span>

                        <input type="checkbox" id="toggle_button" v-model="checkedValue">
                        <span class = "toggle__switch"></span>
                        </label></li>
                    <li><button class="dropdown-edit">edit</button></li>
                    <li><button class = "dropdown-delete">delete</button></li>
                </ul>
            </div>
        </div>
    </section>
</template>

<script>
export default{
  props: {
      defaultState: {
          type: Boolean,
          default: false
      }
  },
    data(){
        return{
            searchQuery:'',
            selectedItems: null,
            isVisible: false, 
            userArray: [],
            currentState: this.defaultState,
        };

    },
    computed: {
        isActive() {
            return this.currentState;
        
        },
        checkedValue: {
            get() {
                return this.defaultState
            },
            set(newValue) {
                this.currentState = newValue;
                this.$emit('change',newValue);
            }
        }

    },
    mounted() {
        fetch("https://jsonplaceholder.typicode.com/users")
        .then(res => res.json())
        .then(json => {
            console.log(json);
            this.userArray = json;
        })
    },


};
</script>


<style scoped lang="scss"> 
.dropdown-wrapper {
    max-width: 350px;
    position: relative;
    margin: 0 auto;

}
.selected-item {
    height: 25px;
    border: 2px solid lightgray;
    border-radius: 5px;
    padding: 5px 15px;
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
        background: color #f1f1f1;;
        cursor:pointer;
        font-size:16px;
        &:hover{
            background: #f1f1f1;
            color:#fff;
            font-weight: bold;
            .dropdown-edit{
                font-size:16px;
                background: #f1f1f1;
            }
            .dropdown-delete{
                font-size:16px;
                background: #f1f1f1;
            }

        }
        
    

    }
    
    }
    .dropdown-edit{
        background:#fff;
        padding:5px;
        border-bottom:1px solid lightgray;
        margin: 4px 2px;
        border-style:none ;
        border-radius: 5% / 50%;
        padding-bottom: 5px;
        
    }
    .dropdown-delete{
        background:#fff;
        padding:5px;
        border-bottom:1px solid lightgray;
        margin: 4px 2px;
        border-style:none ;
        border-radius: 5% / 50%;
        padding-bottom: 5px;
        
    }
    .toggle__button {
    vertical-align: middle;
    user-select: none;
    cursor: pointer;
}
.toggle__button input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 1px;
    height: 1px;
}
.toggle__button .toggle__switch {
    display:inline-block;
    height:12px;
    border-radius:6px;
    width:40px;
    background: #BFCBD9;
    box-shadow: inset 0 0 1px #BFCBD9;
    position:relative;
    margin-left: 10px;
    transition: all .25s;
}

.toggle__button .toggle__switch::after, 
.toggle__button .toggle__switch::before {
    
    content: "";
    position: absolute;
    display: block;
    height: 18px;
    width: 18px;
    border-radius: 50%;
    left: 0;
    top: -3px;
    transform: translateX(0);
    transition: all .25s cubic-bezier(.5, -.6, .5, 1.6);
}

.toggle__button .toggle__switch::after {
    background: #4D4D4D;
    box-shadow: 0 0 1px #666;
}
.toggle__button .toggle__switch::before {
    background: #4D4D4D;
    box-shadow: 0 0 0 3px rgba(0,0,0,0.1);
    opacity:0;
}
    


    
    
}


</style>