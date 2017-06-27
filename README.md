
const express=require("express");
const bodyParser=require("body-parser");
const cookieParser=require("cookie-parser");
const  app=express();
配置模板
app.set("view engine","ejs");
app.set("views","views");
解析urlencoding编码的请求
app.use(bodyParser.urlencoded({extended:false}));
app.use(bodyParser.json());
配置cookie为中间件 主要是解析cookie字符串
app.use(cookieParser());
app.use(express.static("public"));

app.get("/sendCookie",(req,res)=>{
    
    将cookie发送给浏览器,用res.cookie()来设置cookie
    
    res.cookie("username","sunwukong");
    res.cookie("age","18")
    res.send("cookie 已经发送给浏览器了");

});
app.get("/getCookie",(req,res)=>{
    通过request对象来读取cookie
    console.log(req.get("Cookie"))
    需要一个中间件来帮助我们解析cookie
    console.log(req.cookies.username);
    console.log(req.cookies.age)
    res.send("cookie 已经发送给浏览器了");
    });


         Cookie发送给浏览器以后，浏览器会自动保存，
         当再次访问服务器时再将保存的Cookie发回
         而cookie在浏览器中保存是由效期的，一旦超过有效期cookie将会被销毁
        
         默认情况下有效期是一次会话，一旦关闭浏览器则Cookie自动销毁
         （会话指的是一次打开关闭浏览器的过程）
         
        



app.listen(3000,()=>{
    console.log("服务器已经启动")
});
