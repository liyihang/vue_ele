<template>
<div class="shopcart">
    <div class="cart-content">
        <div class="content-left">
            <div class="log-wrapper">
            <div class="logo">
                <span class="icon-shopping-cart"></span>
            </div>
        </div>
        </div>
        <div class="content-right">
            <div class="price"></div>
            <div class="diliver"></div>
        </div>
    </div>
</div>
</template>
<script>
export default {
}
</script>
<style>
.shopcart {
    position: fixed;
    left: 0;
    bottom: 0;
    z-index: 50;
    width: 100%;
    height: 48px;
    background: #000;
}
.cart-content {
    display: flex;
    background: #141d27;
}
.content-left {
    flex: 1
}
.content-left .logo-wrapper {
    display: inline-block;
    position: relative;
    top: -10px;
    margin: 0 12px;
}
.content-right {
    flex: 0 0 105px;
    width: 105px;
}

</style>
