<script>
import '../style.scss'
export default{
    name: "Themeswitch",
    data: () => {
        return{
            isDarkTheme: localStorage.getItem('theme') === 'dark'
        }
    },
    watch: {
        isDarkTheme:{
            handler(val){
                const theme = val ? 'dark' : 'light';
                document.documentElement.setAttribute('data-theme', theme)
                localStorage.setItem('theme', theme);
            },
            immediate: true
        }
    }
}
</script>
<template>
    <div>
        <label>
            <input type="checkbox" v-model="isDarkTheme" class="mr-1">
            <span>Theme Switch</span>
        </label>
    </div>
</template>
<style lang="css"></style>