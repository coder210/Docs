# WebӦ�ó�����Ŀ�ṹһ��

#### һ������.Net Core��WebӦ�ó������Ŀ
��ͼ��ʾ: ��������Ŀ,vs����ֻ�������Զ�������`Program.cs`��`Startup.cs`�����ļ�.������Ŀ������ʮ�ֵĸ�ˬ

![����Ŀ�ṹͼ][empty_project]
<br/>
<br/>

  
##### Program.cs: �ǳ���������  
```c#
// ��ں���
public static void Main(string[] args)
{
	CreateWebHostBuilder(args).Build().Run();
}

// ����һ��web�ķ�����
public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
	WebHost.CreateDefaultBuilder(args)
		.UseStartup<Startup>();
}
```
<br/>

##### Startup.cs: �ǳ����������,��������,���õĶ�ȡ�͸�������ע�붼�����ﴦ��

```c#
// ��������
public void ConfigureServices(IServiceCollection services)
{
}

// http�ܵ�����
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
	// ���Ե���
	if (env.IsDevelopment())
	{
		app.UseDeveloperExceptionPage();
	}

	// ���г���
	app.Run(async (context) =>
	{
		// ��http�����hello world�ַ���
		await context.Response.WriteAsync("Hello World!");
	});
}
```
<br/>

---

<br/>


#### ��������.Net Core��WebӦ�ó���Web API��Ŀ
��ͼ��ʾ: Web API�����Ŀ���,���˴���`Program.cs`��`Startup.cs`�ļ���,��������`appsettings.json`�ļ���Controllers�ļ����µ�`ValuesController.cs`�ļ�.  
ͨ�����־�֪���������ļ�����ʲô����, **appsettings.json**����һЩ����, **ValuesController.cs**ѧ��asp.net mvcһ������Ϥ�ĸо�,�ⲻ����һ����������

![web api�ṹͼ][webapi_project]

<br/>

##### Program.cs: ����������,���������Ŀ���ɵĴ���һëһ��
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

##### Startup.cs: �����������,��������,���õĶ�ȡ�͸�������ע�붼�����ﴦ��
```c#
// �����Ŀ���,�������˹��캯��,���Ҳ����ǹ����������ʵ��
public Startup(IConfiguration configuration)
{
	Configuration = configuration;
}

public IConfiguration Configuration { get; }

public void ConfigureServices(IServiceCollection services)
{
	// .net core��mvc��ͬ��.net framework���ɵ���Ŀ��,�����ǿ����õ�
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
	// ����ӻ�����,��Ҫ����Ҫʹ��mvc
	app.UseMvc();
}
```

<br/>

##### ValuesController.cs: ��������,�Ͳ��ö�˵��,΢�����˼����÷���.net framework��һ�㶼û��, ��Ҳ��������ũ�ĸ��� :smile: :smile: :smile:
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

##### appsettings.json: �����ļ�,ȡ����.net frameworkʱ����app.xml�ļ�,��Ϊ���json��˵,xml̫����
```javascript
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning" // log���Ĭ�ϼ����Ǿ���
    }
  },
  "AllowedHosts": "*" // �������е�ip����
}
```
<br/>

---

<br/>

#### ��������.Net Core��WebӦ�ó���
��ͼ��ʾ: `Startup.cs`, `Program.cs`��`appsetting.json`�Ͳ����ٹ��������, ����Pages�ļ��µ��ļ�, ѧϰ��asp.net mvc��һ������Ϥ��,����û�б�, ����һЩ`Razor`ҳ��, ��ؾ������ݽ�������mvcר��

![��ȫ��WebӦ�ó���][web_project]


<br/>

---

<br/>


### �ܽ�: ���濴����.net core��ԭ�е�.net framework�����кܶ���֮ͬ��,��ζ�����ǵ�ѧϰ�ɱ�������


<!-- ͼƬ���� -->
[empty_project]: ./images/empty-project.png
[webapi_project]: ./images/webapi-project.png
[web_project]: ./images/app.png
