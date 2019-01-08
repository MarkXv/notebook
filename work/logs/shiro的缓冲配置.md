## shiro的缓冲配置


>项目一直在刷:

<code>
	No cache or cacheManager properties have been set.  Authorization cache cannot be obtained
>配置shiro无效
>authRealm.setAuthenticationCachingEnabled(false); 
>


> 使用下面的配置即可实现
<code>

	[main]
	builtInCacheManager = org.apache.shiro.cache.MemoryConstrainedCacheManager
	securityManager.cacheManager = $builtInCacheManager