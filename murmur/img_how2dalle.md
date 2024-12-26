# 關於怎麼讓 ChatGPT 教 DALL-E 畫圖這件事 2024-12-26 18:29

API 請 DALL-E 畫圖是按張數計費。  
當然了，付費服務 ChatGPT pro/workspace 也能畫，這樣做好處是不怕塞車。  
壞處是其實你不太清楚它到底怎麼「翻譯」你的 prompts。  

請不要這樣做：  
```python
gpt_response = gpt_client.images.generate(
    model="dall-e-3",
    quality="standard",
    prompt="繪製代表知識管理系統的 icon",
    size="1024x1024",  # executed in 14.0s, finished 18:36:29 2024-12-26
    n=1,
)
```

這跟 API 呼叫 4o-mini 不太一樣、沒辦法自己設定 system prompt：它會按照自己的翻譯機去畫。  
例如剛剛那段中文指令，實際上在 AI 眼中的 `revised_prompt` 是長這樣的：

```json
{
 "b64_json": "iVBORw0KGgoAAA...(SUPER LONG)",
 "revised_prompt": "Illustrate an icon that represents a knowledge management system. It could be a combination of a book symbolizing knowledge, a gear indicating system, and network lines showcasing management and connectivity.",
 "url": null
}
```

(Work in progress...)