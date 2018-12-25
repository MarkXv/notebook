# 使用Mybatis自关联出现死循环：

> 代码方面没有差错，数据填充时注意，不要出现自己是自己的上级


<code>

	20:13:20.030 [ERROR] [http-nio-8090-exec-10] o.a.catalina.core.ContainerBase.[Tomcat].[localhost].[/].[dispatcherServlet] [DirectJDKLog.java : 182] Servlet.service
	() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is org.springframework.http.converter.HttpM
	essageConversionException: Type definition error: [simple type, class io.fairymagic.exam.api.domain.Organization]; nested exception is com.fasterxml.jackson.databi
	nd.exc.InvalidDefinitionException: Direct self-reference leading to cycle (through reference chain: java.util.ArrayList[1]->io.fairymagic.exam.api.domain.Organizat
	ion["org"]->io.fairymagic.exam.api.domain.Organization["org"])] with root cause
	com.fasterxml.jackson.databind.exc.InvalidDefinitionException: Direct self-reference leading to cycle (through reference chain: java.util.ArrayList[1]->io.fairymag
	ic.exam.api.domain.Organization["org"]->io.fairymagic.exam.api.domain.Organization["org"])




自关联问题
<code>

	<association property="org" column="organization"  select="findOrganizationById" autoMapping="true"></association>

