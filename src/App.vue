<template>
    <div>
        <navbar :pages="pages" :active-page="activePage" :nav-link-click="(index) => activePage = index">
        </navbar>
        <!-- <page-viewer :page="pages[activePage]"
        v-if="pages.length>0">
        </page-viewer> -->

        <create-page @page-created="pageCreated"></create-page>
    </div>
</template>

<script>
import PageViewer from './components/PageViewer.vue';
import Navbar from './components/Navbar.vue';
import CreatePage from './components/CreatePage.vue';
export default {
    components: {
        Navbar,
        PageViewer,
        CreatePage
    },
    created(){
        this.getPages();
    },
    data() {
        return {
            activePage: 0,
            pages: []
        };
    },
    methods:{
        async getPages(){
            let res = await fetch('pages.json');
            let data =await res.json();

            this.pages= data;
        },
        pageCreated(pageObj){
            this.pages.push(pageObj);
        },
    }
};
</script>
