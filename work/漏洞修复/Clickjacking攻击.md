# 应对Clickjacking攻击

> Tomcat的web.xml配置文件中(效果未进行测试)
<code>

	<filter-mapping>
        <filter-name>httpHeadSecurity</filter-name>
        <url-pattern>/*</url-pattern>
        <dispatcher>REQUEST</dipatcher>
    </filter-mapping>