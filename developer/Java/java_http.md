# Http的Java实现

## httpclient

```
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpclient</artifactId>
    <version>4.3.2</version>
</dependency>
```
### 一个简单的post请求
```
// 构建一个请求对象,可以是HttpPost,HttpGet,以及实现了http put和delete的HttpPut, HttpDelete
        HttpPost simplePost  = new HttpPost("http://www.baidu.com/");

// 创建一个默认的客户端
        HttpClient httpClient = HttpClients.createDefault();
        HttpResponse httpResponse = null;
        try {
            //导入或执行你的请求对象
            httpResponse = httpClient.execute(simplePost);
            HttpEntity httpEntity =  httpResponse.getEntity();
            // 获取请求相应的文本
            String result = EntityUtils.toString(httpEntity, Consts.UTF_8);
            System.out.println(result);
        } catch (IOException e) {
            e.printStackTrace();
        }
```
### 添加请求体(body)
http中body 对了包中HttpEntity,不同类型的数据类型,对应了不同的HttpEntiry的实现, 可以参考httpclient包的org.apache.http.client.entity和httpcoreorg.apache.http.entity包内的各种实现. 比较常用的就是StringEntity和UrlEncodedFormEntity了,分别处理文本/Json格式和urlencode-form格式的数据.
```
// 构建一个键/值对形式的参数BasicNameValuePair, 然后通过键值参数构建UrlEncodedFormEntity.
BasicNameValuePair paramsBasePair = new BasicNameValuePair("name","San Zhang");
        List<BasicNameValuePair> paramsBasePairList = new ArrayList<BasicNameValuePair>();
        paramsBasePairList.add(paramsBasePair);
        UrlEncodedFormEntity formEntity = new UrlEncodedFormEntity(paramsBasePairList,Consts.UTF_8);

        // 使用是只需要通过setEntity方法设置请求的body

        HttpPost simplePost  = new HttpPost("http://www.baidu.com/");
        simplePost.setEntity(formEntity);

```