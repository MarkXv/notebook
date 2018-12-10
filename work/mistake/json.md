# 使用Jackson时：
### 1. List的转换时内置转换为HashMap
List<ConsultantDto> myObjects = mapper.readValue(jsonInput, new TypeReference<List<ConsultantDto>>(){});

### 2. jackson 时间处理
    spring.http.converters.preferred-json-mapper = jackson
    
    spring.jackson.date-format = yyyy-MM-dd HH:mm:ss
    spring.jackson.time-zone = GMT+8

### 