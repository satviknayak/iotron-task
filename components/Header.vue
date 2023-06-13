<template>
        <nav id="header" class="flex w-full h-fit p-4 fixed top-0 transition-all duration-500 ease-in-out">
            <div class="flex backdrop-blur-md w-full h-full bg-white/20 border-2 border-white/60 rounded-lg justify-between items-center relative flex-col sm:flex-row p-4">
                <div class="flex justify-between w-full sm:w-fit items-center" >
                    <h2 class="text-2xl text-white"><nuxt-link to="/">LOGO</nuxt-link></h2>
                    <span @click="setshow" :class="[show ? 'hidden':'flex' ]" class="sm:hidden" ><Icon name="heroicons-solid:bars-3" class="text-white text-3xl cursor-pointer" /></span>
                    <span @click="setshow" :class="[show ? 'flex':'hidden' ]"  class="sm:hidden" ><Icon name="heroicons-solid:x-mark" class="text-white text-3xl cursor-pointer"/></span>
                </div>
                <ul :class="[show?'mt-8 sm:mt-0':'hidden sm:flex']" class="flex gap-4 py-4 sm:py-0 text-slate-300 flex-col sm:flex-row items-center w-full sm:w-fit">
                    <li v-for="link in links" :id="link.id" @click="setshow" class="cursor-pointer px-2 py-2 hover:text-slate-100 active:text-white after:content-[''] after:w-full after:bg-slate-100 after:h-1 after:block after:translate-y-2 after:opacity-0 hover:after:translate-y-0 hover:after:opacity-100 transition-all duration-750 ease-in-out after:transition-all after:duration-750 after:ease-in-out"><nuxt-link class="active:text-slate-100" :to="link.link">{{ link.title }}</nuxt-link></li>
                </ul>
                
            </div>
        </nav>
</template>

<script setup>
    import { useWindowScroll } from '@vueuse/core'

    const { x, y } = useWindowScroll()
    
    const show = useState('show',()=>false);
    const setshow = () => {
        show.value = !show.value;
    }
    const links = useState('links',()=>[
        {title:'Home',link:'/'},
        {title:'About',link:'/about'},
        {title:'Docs',link:'/docs'},
        {title:'Contact',link:'/contact'},
    ]);
    const prevScrollpos = useState('prevScrollpos', () => y);
    onMounted(() => { 
        window.onscroll = function() {
            const currentScrollPos = useState('currentScrollpos', () => y);
            if ((prevScrollpos.value > currentScrollPos.value)||show.value) {
                document.getElementById("header").style.top = "0";
            } else {
                document.getElementById("header").style.top = "-150px";
            }
            prevScrollpos.value = currentScrollPos.value;
        };
    })    
</script>