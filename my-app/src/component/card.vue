<template>
    <div>
        <f7-card>
            <f7-card-header>
                <div class="avatar">
                    <img width="34" height="34" :src="data.avatar">
                </div>
                <div class="username">{{data.username}}</div>
                <div class="userdate">{{data.userdate}}</div>
            </f7-card-header>
            <f7-link @click="contentclick(data)">
            <f7-card-content  v-if="data.type=='text'" class="text">
                {{data.text}}
            </f7-card-content>
            <f7-card-content v-if="data.type=='mp4'" class="text">
                <videoVue :data="data.text"></videoVue>
            </f7-card-content>
            <f7-card-content v-if="data.type=='pic'" class="text pic">
                <div>{{data.text}}</div>
                <img :src="data.pic" alt="">
            </f7-card-content>
            </f7-link>
<!--             <f7-link v-if="data.type=='mp4'" @click="videoclick">
                <div style="float:left;width:49%;border:1px solid #fff;">
                      <my-video :sources="video.sources" :options="video.options"></my-video>
                </div>
            </f7-link> -->
            <f7-card-footer v-if="enableToolbar" >
                <f7-link @click="dianzan">
                    <span class="iconfont icon-iconlikenum" ></span>
                    <span id="zan">赞</span>
                </f7-link> 
                <f7-link>
                    <span class="iconfont icon-buxihuan"></span>
                    <span>踩</span>
                </f7-link> 
                <f7-link>
                    <span class="iconfont icon-pinglun"></span>
                    <span>评论</span>
                </f7-link> 
                <f7-link>
                    <span class="iconfont icon-fenxiang"></span>
                    <span >分享</span>
                </f7-link>                                  
            </f7-card-footer>
        </f7-card>
    </div>
</template>
<script>
    import header_data from '../json/header_data.json'
    import videoVue from '../component/video.vue'
    export default{
        props:{
            data:{
                default:""
            },
            enableToolbar:{
                type:Boolean,
                default:true
            }
        },
        data(){
            return {
                // msg:'',
            }
        },
        methods: {
            dianzan(){
                var zan = document.getElementById('zan');
                if(zan.innerHTML == "赞"){
                    zan.innerHTML = "已赞";
                }else{
                    zan.innerHTML = "赞";
                }
            },
            contentclick(data){
                this.$emit('card:content-click', data);
            },
            videoclick(){
                  this.$f7.mainView.router.load({url:'/video/'})
            }
        },
        mounted(){
            // bus.$on('qq', (text) => { //Hub接收事件
            //     this.msg = text
            // })
        },
        components: {
            videoVue
        }
    }
</script>
<style scoped>
    .card-header{
        display:block;
    }
    .avatar{
        float:left;
    }
    .username{
        margin-left:44px;
        font-size:14px;
        font-weight:500;
    }
    .userdate{
        margin-left:44px;
        font-size:13px;
        color:#8e8e93;
    }
    .pic img{
        width:100%;
    }
</style>