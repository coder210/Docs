# Web应用程序项目结构一览

#### 一、创建.Net Core的Web应用程序空项目
如图所示: 创建空项目,vs编译只给我们自动生成了`Program.cs`和`Startup.cs`两个文件.整个项目看起来十分的干爽

![空项目结构图][empty_project]
<br/>
<br/>

  
##### Program.cs: 是程序的入口类  
```c#
// 入口函数
public static void Main(string[] args)
{
	CreateWebHostBuilder(args).Build().Run();
}

// 创建一个web的服务器
public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
	WebHost.CreateDefaultBuilder(args)
		.UseStartup<Startup>();
}
```
<br/>

##### Startup.cs: 是程序的启动类,服务启动,配置的读取和各种依赖注入都在这里处理

```c#
// 服务配置
public void ConfigureServices(IServiceCollection services)
{
}

// http管道配置
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
	// 调试调用
	if (env.IsDevelopment())
	{
		app.UseDeveloperExceptionPage();
	}

	// 运行程序
	app.Run(async (context) =>
	{
		// 往http中输出hello world字符串
		await context.Response.WriteAsync("Hello World!");
	});
}
```
<br/>

---

<br/>


#### 二、创建.Net Core的Web应用程序Web API项目
如图所示: Web API与空项目相比,除了创建`Program.cs`和`Startup.cs`文件外,还创建了`appsettings.json`文件和Controllers文件夹下的`ValuesController.cs`文件.  
通过名字就知道这两个文件是做什么的了, **appsettings.json**存了一些配置, **ValuesController.cs**学过asp.net mvc一定有熟悉的感觉,这不就是一个控制器类

![web api结构图][webapi_project]

<br/>

##### Program.cs: 程序的入口类,并且与空项目生成的代码一毛一样
```c#
public static void Main(string[] args)
{
	CreateWebHostBuilder(args).Build().Run();
}

public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
	WebHost.CreateDefaultBuilder(args)
		.UseStartup<Startup>();
```

<br/>

##### Startup.cs: 程序的启动类,服务启动,配置的读取和各种依赖注入都在这里处理
```c#
// 与空项目相比,多生成了构造函数,而且参数是管理配置类的实例
public Startup(IConfiguration configuration)
{
	Configuration = configuration;
}

public IConfiguration Configuration { get; }

public void ConfigureServices(IServiceCollection services)
{
	// .net core的mvc不同于.net framework集成到项目中,这里是可配置的
	services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
	if (env.IsDevelopment())
	{
		app.UseDeveloperExceptionPage();
	}
	else
	{
		app.UseHsts();
	}

	app.UseHttpsRedirection();
	// 光添加还不行,还要表明要使用mvc
	app.UseMvc();
}
```

<br/>

##### ValuesController.cs: 控制器类,就不用多说了,微软做了兼容用法和.net framework上一点都没变, 这也是我们码农的福音 :smile: :smile: :smile:
```c#
// GET api/values
[HttpGet]
public ActionResult<IEnumerable<string>> Get()
{
	return new string[] { "value1", "value2" };
}

// GET api/values/5
[HttpGet("{id}")]
public ActionResult<string> Get(int id)
{
	return "value";
}
```
<br/>

##### appsettings.json: 配置文件,取代了.net framework时代的app.xml文件,因为相对json来说,xml太重了
```javascript
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning" // log输出默认级别是警告
    }
  },
  "AllowedHosts": "*" // 允许所有的ip访问
}
```
<br/>

---

<br/>

#### 三、创建.Net Core的Web应用程序
如图所示: `Startup.cs`, `Program.cs`和`appsetting.json`就不用再过多解释了, 对于Pages文件下的文件, 学习过asp.net mvc的一定很熟悉了,基本没有变, 就是一些`Razor`页面, 相关具体内容解释留到mvc专题

![最全的Web应用程序][web_project]


<br/>

---

<br/>


### 总结: 表面看起来.net core与原有的.net framework还是有很多相同之处,意味着我们的学习成本降低了


<!-- 图片链接 -->
[empty_project]: ./images/empty-project.png
[webapi_project]: ./images/webapi-project.png
[web_project]: ./images/app.png
