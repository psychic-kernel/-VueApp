<script>
import { RouterLink, RouterView } from 'vue-router';
import UtilBar from '@/components/UtilBar.vue';
export default {
    data(){
        return {
            isActive: false,
            iconBars: ['fas', 'bars'],
            iconClose: ['fas', 'xmark']
        }
    },
    methods: {
        toggleUtils(){
            return this.isActive = !this.isActive;
        }
    },
    components: {
        UtilBar
    }
}

</script>

<template>
    
    <router-view/> 
    <ul class="navbar">
        <span id="utilToggler"> 
            <font-awesome-icon class="util-toggler" :icon="iconBars"
            @click="toggleUtils()"/>
        </span>
        <li><router-link class="link" to="/">Home</router-link></li> 
        <li><router-link class="link" to="/about">About</router-link></li>
        <li><router-link class="link" to="/gallery">Gallery</router-link></li>
        <li><router-link class="link" to="/vue-docs">Vue Docs</router-link></li>
    </ul>
    <div v-show="isActive">
        <span id="utilToggler"> 
            <font-awesome-icon class="util-toggler" :icon="iconClose"
            @click="toggleUtils()"/>
        </span>
        <util-bar class="utilbar"/>
    </div>
   
    <!-- <slot/> -->
      
</template>

<style scoped>
.navbar {
    position: fixed;
    display: flex;
    width: 100%;
    height: 50px;
    top: 0;
    gap: 15px; 
    list-style-type: none;
    background-color: var(--bg-color-nav);
    
}

span .util-toggler {
    position: relative;
    height: 2.5em;
    padding: 1px;
    left: 5px;
    top: 3px;
    color: var(--text-color-nav);
    z-index: 1000;

}
span .util-toggler:hover{
    background-color: var(--bg-menu-hover);
    cursor: pointer;
    
}
span .util-toggler:active{
    background-color: transparent;
}

li > .link {
    font-size: 18pt;
    /* margin-top: 1em; */
    color: var(--text-color-nav);
    margin-left: 10px;
}
li > .link:hover {
    text-decoration: none;
}


</style>