<template>
    <div>
        <detail-banner 
            :sightName="sightName" 
            :bannerImg="bannerImg" 
            :bannerImgs="gallaryImgs">
        </detail-banner>
        <detail-header></detail-header>
        <detail-list :list = 'list'></detail-list>
    </div>  
</template>

<script>
import DetailBanner from './components/Banner'
import DetailHeader from './components/Header'
import DetailList from './components/List'
import axios from 'axios'
export default{
    name: 'detail',
    components:{
        DetailBanner,
        DetailHeader,
        DetailList,
    },
    data () {
        return {
            sightName: '',
            bannerImg: '',
            gallaryImgs: [],
            list: []
        }
    },
    methods: {
        getDetailInfo () {
            axios.get('/api/detail.json', {
                params: {
                    id: this.$route.params.id
                }
        }).then(this.handleGetDataSucc)
    },
    handleGetDataSucc (res) {
        res = res.data
        // console.log(res);
        
        if (res.ret && res.data) {
            const data = res.data
            this.sightName = data.sightName
            // console.log(data.sightName)
            this.bannerImg = data.bannerImg
            // console.log(data.bannerImg)
            this.gallaryImgs = data.gallaryImgs
            this.list = data.categoryList
        }
    }
  },
  mounted () {
    this.getDetailInfo()
    console.log(this.$route.params.id)
  }
}
</script>

<style>

</style>
