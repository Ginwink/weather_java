# weather_java
andorid_java

#### 介绍
andorid学习项目天气App

#### 软件架构
软件架构说明
获取API接口使用okHttp3

     private void sendRequestWithOkHttp() {  
     new Thread(new Runnable() {  
     @Override  
     public void run() {  
     String url = "http://apis.juhe.cn/simpleWeather/query";  
     String key = "***"; // 替换为您的API密钥  
     String city = "上海"; //替换为您的key 
     mcity.setText(city);  
     OkHttpClient client = new OkHttpClient();
    
    Request request = null;  
    try {  
    request = new Request.Builder()  
    .url(url + "?" + "city=" + URLEncoder.encode(city, "UTF-8") + "&" + key)  
    .build();  
    } catch (UnsupportedEncodingException e) {  
    throw new RuntimeException(e);  
    }
         try (Response response = client.newCall(request).execute()) {
                        if (!response.isSuccessful())
                            throw new IOException("Unexpected code " + response);
    
                        String responseData = response.body().string();
                        JSONObject jsonObject = new JSONObject(responseData);
    
                        // 解析JSON
                        JSONObject result = jsonObject.getJSONObject("result");
                        JSONObject realtime = result.getJSONObject("realtime");
                        JSONArray future = result.getJSONArray("future");
    
                        // 提取数据
    //                  cityId = realtime.getString("city");
                        temperature = realtime.getString("temperature");
                        humidity = realtime.getString("humidity");
                        direct = realtime.getString("direct");
                        power = realtime.getString("power");
                        info = realtime.getString("info");
    
                        // 更新UI
                        runOnUiThread(() -> showResPonse(temperature, info, direct, temperatures, humidity, power));
                    } catch (IOException | JSONException e) {
                        e.printStackTrace();
                    }
                }
            }).start();
        }


#### 使用说明

***仅提供学习借鉴使用***
//写的不是很好

#### 使用说明
API来自聚合数据
url = https://www.juhe.cn

需要自己登录获取API以及key
