<template>
<div id="wrapper">
    <div id="content">
        <header class="default heade-sticky">
            <div class="un-title-page go-back">
                <a @click="$nuxt.$router.back()" class="icon">
                    <i class="ri-arrow-drop-left-line"></i>
                </a>
            </div>
            <div class="un-block-right">
                <div class="btn-like-click shape-box">
                    <div class="btnLike">
                        <input type="checkbox" :checked="this.$store.state.currentNFT.like ? 'checked' : ''">
                        <div class="icon-inside">
                            <i class="ri-heart-3-line"></i>
                        </div>
                    </div>
                </div>
            </div>
        </header>
        <div class="space-sticky"></div>
        <Nuxt />
    </div>
    <BidModal/>
</div>
</template>

<script>
export default {
    methods: {
    }
}
</script>