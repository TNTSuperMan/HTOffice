<script setup>
import Home from "../hbtn.vue";
</script>
<template>
    <Home color="#000"/>
    <dl>
        <div>
            <dt>Vue</dt>
            <dd><a target="_blank" href="https://github.com/vuejs/vue/blob/main/LICENSE">MITライセンス下に公開されています</a></dd>
        </div><br>
        <div>
            <dt>Vite</dt>
            <dd><a target="_blank" href="https://github.com/vitejs/vite/blob/main/LICENSE">MITライセンス下に公開されています</a></dd>
        </div><br>
        <div>
            <dt>ホームアイコン</dt>
            <dd><a target="_blank" href="https://www.svgrepo.com/svg/522409/home">CC BY下に提供されています。</a><br>
                <span>以下の変更があります：</span>
                <ul>
                    <li>/src/hbtn.vueに埋め込みました</li>
                    <li>背景を削除しました</li>
                    <li>色をv-bindさせました</li>
                </ul>
            </dd>
        </div>
    </dl>
</template>
<style scoped>
dl{
    text-align:center;
}
</style>