### swaggerһ��������ʹ��
һ������swagger������Ŀ,����ѡ��ʹ��**ASP.NET Web Api** ���ɵ���Ŀ�ṹ����:

![](images/dev_dir.png)

����ʹ��Nuget��������װ***swashbuckle***

![](images/dll_detail.png)


������װ�ɹ�֮��,���������Ŀ������һ��**SwaggerConfig.cs**����,������Swagger���õĵط�
```c#
// �����ĵ��İ汾
c.SingleApiVersion("v1", "SwaggerTest");

// ���ĵ����ע��,�ӿո�xml�ĵ��ж�ȡע����Ϣ
 c.IncludeXmlComments(string.Format("{0}/bin/WebAPI.xml", System.AppDomain.CurrentDomain.BaseDirectory));

 // ��ֹ�������ر���
c.ResolveConflictingActions(apiDescriptions => apiDescriptions.First());
```


�ġ�����Ŀ���һ�->����->����->��xml�ĵ��ļ���ѡ��

![](images/xml.png)


�塢�������֮�����в鿴swagger�ṩ�����ߵ�ַ����

http://domain/swagger/ui/index#/



