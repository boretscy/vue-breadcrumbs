<template>
    <div class="container mt-5 mb-3 breadcrumbs">
        <div class="row">
            <div class="col text-minus">
                <item 
                    v-for="(item, indx) in items"
                    :key="indx"
                    :item="item"
                    :first="indx == 0"
                    :last="indx == items.length-1"
                    />
            </div>
        </div>
    </div>
</template>

<script>
import Item from '@/components/Item.vue'

export default {
    name: 'YAppBreadcrumbs',
    components: {
        Item
    },
    data() {
        return {
            external: document.getElementById('YAppsBreadcrumbs').getAttribute('items') || null,
            local: localStorage.getItem('CIS_NAV') || null,
            internal: []
        }
    },
    computed: {
        items: function() {
            let s = [], l = JSON.parse(this.local), e = JSON.parse(this.external)
            
            e.forEach( (i) => {
                s.push({title: i.TITLE, link: i.LINK})
            })
            if ( l.brand ) s.push({title: l.brand.name, link: e[e.length-1].LINK+l.brand.code})
            if ( l.model ) s.push({title: l.model.name, link: e[e.length-1].LINK+l.brand.code+'/'+l.model.code})
            if ( l.item ) s.push({title: l.item, link: null})

            return s
        }
    },
    mounted: function() {
        
        setInterval(() => {
            if ( this.local != localStorage.getItem('CIS_NAV') ) {
                this.local = localStorage.getItem('CIS_NAV')
                this.internal = JSON.parse(this.local)
            }
        }, 100);
    }
}
</script>

