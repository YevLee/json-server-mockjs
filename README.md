# 全局安装
cnpm install json-sever -g

# 安装全局依赖
cnpm install

# 配置package.json命令
 "scripts": {
    "dev":"json-server index.js -p 3003",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
  
 # 运行项目
  npm run dev启动项目
  
 # 自定义api
 
// 引入mockjs
// const Mock = require('mockjs');
import Mock from "mockjs"
// 获取 mock.Random 对象
const Random = Mock.Random;
// mock一组数据
const productData = function() {
  let Data = [];
  for (let i = 0; i < 100; i++) {
    let data = {
      name: Random.cname(), // Random.cname() 随机生成一个常见的中文姓名
      date: Random.date()  // Random.date()指示生成的日期字符串的格式,默认为yyyy-MM-dd
    }
    Data.push(data)
  }
 
  return  {
		Data:Data
	}
}
 /*
 @url:自定义接口
 @post/get:自定义请求方式
 @productData：mockjs生成的返回数据
 */
// Mock.mock( url, post/get , 返回的数据)；
Mock.mock('https:test.cn/user/login', 'post', productData );


# 在vue使用
<script>
	import userData from "../data/user.js"
	export default{
		mounted(){
			this.axios.post("https:test.cn/user/login")
			.then(res=>{
				console.log(res)
			})
			.catch(err=>{
				console.log(err)
			})
		}
	}
</script>
