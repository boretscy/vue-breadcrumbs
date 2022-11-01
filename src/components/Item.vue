<template>
    <div 
        class="breadcrumbs-item" 
        :itemprop="( !last ) ? 'itemListElement' : false" 
        :itemscope="!last" 
        :itemtype="( !last ) ? 'http://schema.org/ListItem': false">
        <svg xmlns="http://www.w3.org/2000/svg" v-if="!first"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#arrow-left"></use></svg>
        <a :href="item.link" :title="item.title" itemprop="item" class="text-decoration-none c-yamiddlegray c-h-yablue" v-if="!last">
			<span itemprop="name">{{ item.title }}</span>
		</a>
        <span v-else>{{ item.title }}</span>
        <meta itemprop="position" :content="key+1" v-if="!last">
    </div>
</template>

<script>
export default {
    name: 'Item',
    props: {item: Object, first: Boolean, last: Boolean, key: Number},
}
</script>


<style scoped>
.breadcrumbs svg {
    fill: var(--yablue);
    width: 15px;
    height: 15px;
    margin: 0 10px;
}
.breadcrumbs-item {
    display: inline-block;;
}
</style>