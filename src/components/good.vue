<!--单独商品-->
    <template>
    <div class="Contain">
        <div class="ContainContent">
            <router-link :to="geturl()"><img :src="this.gooditem.pict1" alt=""></router-link>
            <p>{{gettitle()}}</p>
            <p>{{this.gooditem.price}}</p>
            <p>{{this.gooditem.detail}}</p><!--差值表达式-->
        </div>
    </div>
</template>

<script>
export default {
    props:["goodid"],
    data(){
        return {
            gooditem:"",
        }
    },
created(){
     // 获取本地JSON文件
      axios.get("static/goodlist.json").then((res)=>{
        this.gooditem = res.data.goods[this.goodid-1];
      })
  },
  methods:{
    geturl(){
        return "/GoodDetail"+(this.goodid-1);
    },
    gettitle(){
        return this.gooditem.title.slice(0,28)//slice控制对象title的长度为0到28(title文字长短不一导致布局上下不对齐)
    }
  }
}
</script>

<style scoped>
.Contain{
    width: 230px;
    height: 400px;
    margin-right: 10px;
    margin-bottom: 10px;
    display: inline-block;
    background-color: cornflowerblue;
}
.ContainContent img {
    width: 220px;
    height: 220px;
}
</style>