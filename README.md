<h1 align="center">AtomBulb</h1>
<h4 align="center">
    <p>
        <a href="">English</a> |
        <b>中文</b>
    <p>
</h4>

### Bulb<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/qinwei/bulb_icon.svg width=30 height=30 /> 项目的愿景
在这个颠覆时代的AI技术浪潮中，国内外涌现出了一大批有影响力和代表性的大模型产品，包括但不限于：
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/gpt.svg width=30 height=30 /> OpenAI的ChatGPT
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/chatglm.svg width=25 height=30 /> &nbsp; 智谱AI的ChatGLM
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/mianbi.svg width=30 height=30 /> 面壁智能的面壁模方
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/yiyan.svg width=30 height=30 /> 百度的文心一言
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/tongyi.svg width=22 height=22 /> &nbsp; 阿里的通义千问
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/xinghuo.svg width=30 height=30 /> 讯飞的星火大模型


我们尝试和这些未来的AGI对话，去了解它们的所思所想，打破人类和AGI之间的认知隔阂。[**Bulb**](https://bulb.atomecho.cn/)项目的名称意为“灯泡”，旨在为大型模型产品的能力边界照亮明灯，以便我们能够对它们有更具体和定量的认识。在我们的官网获取更详细的信息：https://bulb.atomecho.cn

未来，我们会不断为大模型家庭引入新的成员。为了能够更公平地去探索各个大模型的能力，我们为每个大模型起了个别名，包括：
<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Radish.svg width=30 height=30 />萝卜、<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Eggplant.svg width=30 height=30 />茄子、<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Carrot.svg width=30 height=30 />胡萝卜、<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Chili.svg width=30 height=30 />辣椒、<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Pumpkin.svg width=30 height=30 />南瓜、<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Potato.svg width=30 height=30 />土豆等。

### 数据介绍：
**问题分类信息**：数据包含在question.json
```
 "qid": 问题编号
 "question": 问题描述
 "first_level_class": 一级分类
 "second_level_class": 二级分类
```
例如：
```
[
    {
        "qid": 0,
        "question": "请你写出一个可以生成五个不同随机数的 Python 程序。",
        "first_level_class": "代码编程",
        "second_level_class": "代码生成"
    },
	...
]
```

**问题回答信息**：数据包含在每个模型目录下的answer-<日期>.json，其中“日期”字段表示该份答案获取的具体时间，方便我们对应到具体的模型版本。在answer-<日期>.json中，具体的字段信息如下，我们之后会进一步扩展用户的反馈数据：
```
 "qid": 问题编号
 "answer": 模型回答
```
```
[
    {
        "qid": 0,
        "answer": "请你写出一个可以生成五个不同随机数的 Python 程序。",
    },
	...
]
```

### 如何评价大模型的能力：
由于大模型在不同任务、知识上具有超强的通用能力，如何客观、准确地评价它们是一个巨大的挑战。为此，我们采取两种方式：
1. 通过OpenAI的GPT-3.5/GPT-4来评分：GPT-3.5/GPT-4是目前大家公认的能力最强的大模型，因此，我们用GPT-3.5/GPT-4来评价各个模型的问答效果。后期，我们会全部采用GPT-4进行评测。我们采用以下格式来对GPT-3.5/GPT-4提问：
```
您是一个乐于助人和准确的助理，用于检查回复具体问题的答案的质量。
[问题]：{question}
[答案]：{answer}
我们希望您对某个AI助手在上述问题的回答表现提供反馈。你将根据从0到10的评分获得总体综合表现得分，其中较高的分数表示整体表现更好。请首先输出一行单独包含一个数值，表示助手的得分。接下来的一行，请提供您评价的全面解释，避免任何潜在的偏见。
```
上面的prompt中，`{question}`和`{answer}`分别对应着被测试的问题内容和大模型的回复。我们举一个具体的例子如下：
```
您是一个乐于助人和准确的助理，用于检查回复具体问题的答案的质量。
[问题]：给出五个原创的古诗或现代诗句子。
[答案]：1. 古诗：春风又绿江南岸，明月何时照我还。\n现代诗：春风吹拂着江南岸，明月何时才能再次照亮我的心房。\n2. 古诗：山重水复疑无路，柳暗花明又一村。\n现代诗：山峦重叠，江水回旋，我心中充满了疑惑和迷茫，但是当我走过一条小巷时，眼前豁然开朗，仿佛又回到了一个美丽的村庄。\n3. 古诗：落霞与孤鹜齐飞，秋水共长天一色。\n现代诗：夕阳的余晖和孤独的野鸟一同飞翔，秋日的湖水和天空融为一体，形成了一幅壮丽的画面。\n4. 古诗：人生若只如初见，何事秋风悲画扇。\n现代诗：如果人生只是初次相见那样简单，那么为什么秋风会让人感到悲伤呢？或许是因为我们经历了太多的离别和分别。\n5. 古诗：采菊东篱下，悠然见南山。\n现代诗：在东边的篱笆下采摘着菊花，悠闲地看着南山，这是一种多么美好的生活啊！
我们希望您对某个AI助手在上述问题的回答表现提供反馈。你将根据从0到10的评分获得总体综合表现得分，其中较高的分数表示整体表现更好。请首先输出一行单独包含一个数值，表示助手的得分。接下来的行，请提供您评价的全面解释，避免任何潜在的偏见。
```

2. 通过用户的反馈来评分：在每个问题的答案下方，我们展示了不同模型的回答，用户可以“点赞”或“点踩”每个答案。我们将统计每个模型的答案得分进行评价，这是一种最为客观和准确的评价方式，但是依赖于大量的用户反馈。因此，我们欢迎每一位朋友在答案下方给出您的评价，您的反馈将影响未来AGI的发展方向。

### 从哪些方面评价大模型
根据我们对大量开源问答数据、社交媒体、论坛、书籍的整理（例如：BELLE、十万个为什么、弱智吧等），经过反复的讨论和梳理，最终设计了八个大的类别来探索大模型的能力，包括：通用知识、语言理解、创作能力、逻辑推理、代码编程、工作技能、使用工具、人格特征。在每个大的类别下又细分了不同的子类，以尽可能全面地覆盖大模型的能力范畴。具体对于每个类别的详细介绍如下，我们也欢迎大家集思广益，让这个分类体系更加全面和准确。

<table class="tg">
<thead>
  <tr>
    <th class="tg-acrh" colspan="2">通用知识：通用知识涵盖了基础科学、数学、历史文化、语言文学、社会科学、日常生活技能以及现代技术应用等多个方面的基本概念和信息。</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">社会人文</td>
    <td class="tg-0pky">社会人文知识包括历史、哲学、语言文学、艺术、宗教、社会学、人类学、政治学、法律、经济学等多个学科领域，以及这些领域中对人类社会、文化、价值观、行为和思维方式的研究和理解。</td>
  </tr>
  <tr>
    <td class="tg-0pky">自然科学</td>
    <td class="tg-0pky">自然科学知识包括物理学、化学、生物学、地理学、地质学、天文学等多个学科领域的系统性知识和方法。</td>
  </tr>
  <tr>
    <td class="tg-0pky">生活常识</td>
    <td class="tg-0pky">生活常识知识包含日常生活、饮食营养、居家安全、交通出行等方面的实用信息和技巧，以帮助人们的日常生活更加便捷、健康和安全。</td>
  </tr>
  <tr>
    <td class="tg-0pky">艺术创作<br></td>
    <td class="tg-0pky">艺术创作知识包含绘画、雕塑、摄影、音乐、舞蹈、戏剧、电影等各种艺术形式的创作技巧、原理和审美理念。</td>
  </tr>
  <tr>
    <td class="tg-0pky">经济</td>
    <td class="tg-0pky">经济学的常识包括了解供求关系，市场经济原理，财政和货币政策，消费者和生产者行为，以及基本的宏观经济指标如GDP，通货膨胀率，失业率等。</td>
  </tr>
  <tr>
    <td class="tg-0pky">时效信息</td>
    <td class="tg-0pky">时效信息包含了具有特定时间限制或与特定时间段相关的事件、数据、趋势、新闻和科技更新等内容。</td>
  </tr>
  <tr>
    <td class="tg-0pky">技术</td>
    <td class="tg-0pky">技术知识包括了对各类现代科技设备的操作和应用，如计算机硬件和软件、互联网技术、移动通信、人工智能、数据分析、机器学习、电子商务、科技创新以及相关的行业和法规标准等方面的理解和技能。</td>
  </tr>
  <tr>
    <td class="tg-0pky">医疗健康</td>
    <td class="tg-0pky">医疗健康知识涵盖了疾病预防、诊断、治疗、康复、身心健康、营养饮食等多方面的医学专业知识和实用技巧。</td>
  </tr>
  <tr>
    <td class="tg-ik58" colspan="2">语言理解：语言理解涵盖了词汇、语法、句法、语义、修辞、语境、非言语线索等多个方面的理解，以及如何将这些组合起来理解和解释口头或书面语言的含义和目的。</td>
  </tr>
  <tr>
    <td class="tg-0lax">翻译</td>
    <td class="tg-0lax">翻译是将一种语言的文本或语音准确、完整地转化为另一种语言的过程，旨在跨越语言障碍，传递和交流信息、文化和思想。</td>
  </tr>
  <tr>
    <td class="tg-0lax">语法词汇</td>
    <td class="tg-0lax">语法词汇能力包括掌握一种语言中的单词、短语、句子结构规则以及运用这些规则正确表达意思的能力。</td>
  </tr>
  <tr>
    <td class="tg-0lax">摘要总结</td>
    <td class="tg-0lax">摘要总结能力包含了提取关键信息、归纳主要观点、整合核心要素、精简表达和呈现内容的能力。</td>
  </tr>
  <tr>
    <td class="tg-0lax">信息抽取</td>
    <td class="tg-0lax">信息抽取能力包含实体识别、关系抽取、事件抽取和属性抽取等关键信息识别和关联技术。</td>
  </tr>
  <tr>
    <td class="tg-0lax">情感分类</td>
    <td class="tg-0lax">情感分类能力包含了识别、分析和理解文本中的情绪、态度和观点等信息。</td>
  </tr>
  <tr>
    <td class="tg-0lax">主题分类</td>
    <td class="tg-0lax">主题分类能力包括对文本、文章或其他信息内容进行识别、分析和归类，以便根据不同主题或领域进行有效组织和检索。</td>
  </tr>
  <tr>
    <td class="tg-0lax">阅读理解</td>
    <td class="tg-0lax">阅读理解能力包含从文本中提取关键信息、理解主旨、分析推理、批判评估以及整合与应用知识等各个方面的技能。</td>
  </tr>
  <tr>
    <td class="tg-740h" colspan="2">创作能力：创作能力指通过创新思维和知识技能，产生独特和有价值的新作品或新想法的能力，能够自动生成富有创意、连贯、可读性较高的文本作品。</td>
  </tr>
  <tr>
    <td class="tg-0lax">文学创作</td>
    <td class="tg-0lax">文学创作是通过文字表达思想、情感和想象力，创作出独特的故事、诗歌和戏剧等艺术作品的过程。</td>
  </tr>
  <tr>
    <td class="tg-0lax">创意文案</td>
    <td class="tg-0lax">创意文案是通过独特的思维和文字表达，为品牌、产品或服务提供引人入胜的广告和推广信息，从而吸引受众关注并激发购买欲望的一种文艺创作方式。</td>
  </tr>
  <tr>
    <td class="tg-0lax">专业文稿</td>
    <td class="tg-0lax">专业文稿是针对特定领域或主题的高质量、准确、严谨的书面材料，用于传达专业知识、观点或信息，例如新闻报道、产品说明、工作汇报等。</td>
  </tr>
  <tr>
    <td class="tg-0lax">风格迁移</td>
    <td class="tg-0lax">文本风格迁移是一种将给定文本的风格或语义特征转移到另一份文本上的能力，例如转换叙述语气、模拟不同作者的叙述方式。</td>
  </tr>
  <tr>
    <td class="tg-0lax">续写扩写</td>
    <td class="tg-0lax">续写扩写是在已有的文本基础上，延伸其情节、创意或主题，形成更长或更完整的作品。</td>
  </tr>
  <tr>
    <td class="tg-nltl" colspan="2">逻辑推理：逻辑推理能力是指通过分析和理解已知的事实或信息，以合理、系统的方式推导出新的信息或结论的能力。</td>
  </tr>
  <tr>
    <td class="tg-0lax">数学</td>
    <td class="tg-0lax">数学能力是指模型理解和处理数学问题的能力，包括执行基本的数学运算，理解和应用数学概念，以及进行复杂的数学推理和解决数学问题。</td>
  </tr>
  <tr>
    <td class="tg-0lax">思辨</td>
    <td class="tg-0lax">思辨能力是指模型在接收到信息或问题时，能够进行分析、批判和推理，从而生成有深度、有洞见的回答或观点，这要求模型能够理解复杂的概念和问题，并能在一定程度上模拟人类的思考过程。同时，需要模型对于一些诡辩或者逻辑混淆的问题能够有效理解和识别。</td>
  </tr>
  <tr>
    <td class="tg-0lax">分析</td>
    <td class="tg-0lax">分析能力是指模型对输入的信息进行深入理解，发现其中的模式和结构，通过推理和逻辑进行处理，并能生成有见地的、结构化的输出或答案，一般的分析问题具有较为复杂的逻辑推理流程。</td>
  </tr>
  <tr>
    <td class="tg-u287" colspan="2">代码编程：代码编程能力是指理解、设计和实现计算机程序的能力，包括熟悉编程语言、逻辑思维、问题解决和代码组织的能力。</td>
  </tr>
  <tr>
    <td class="tg-0lax">代码生成</td>
    <td class="tg-0lax">代码生成指根据给定的问题描述，生成特定语言的程序源代码，例如Python、C、Java、Go、SQL等。</td>
  </tr>
  <tr>
    <td class="tg-0lax">代码纠错</td>
    <td class="tg-0lax">代码纠错是通过检查、发现并修正编程代码中的错误、缺陷或不符合预期功能的过程。</td>
  </tr>
  <tr>
    <td class="tg-0lax">代码解释</td>
    <td class="tg-0lax">代码解释是理解程序源代码并给出自然语言描述，解释代码的功能和执行的操作，或者给出代码段的注释。</td>
  </tr>
  <tr>
    <td class="tg-0lax">代码优化</td>
    <td class="tg-0lax">代码优化是通过对程序代码进行修改和调整，以提高程序运行效率、减少内存占用、降低程序复杂度和提高可读性的过程。</td>
  </tr>
  <tr>
    <td class="tg-cxgh" colspan="2">工作技能：工作技能是指在职业领域中为有效完成特定任务所需的知识、能力和经验。</td>
  </tr>
  <tr>
    <td class="tg-0lax">组织策划</td>
    <td class="tg-0lax">组织策划是对一项活动或项目的目标、流程、资源、参与者等进行系统规划和设计的过程。</td>
  </tr>
  <tr>
    <td class="tg-0lax">营销运营</td>
    <td class="tg-0lax">营销运营是通过有针对性的策划、执行和优化组织的市场活动，以提升品牌知名度、增加客户参与度和推动销售业绩的一种业务管理过程。</td>
  </tr>
  <tr>
    <td class="tg-0lax">协作沟通</td>
    <td class="tg-0lax">协作沟通是一种有效地在团队内部分享信息、观点和建议，以便共同达成目标和解决问题的互动性交流方式。</td>
  </tr>
  <tr>
    <td class="tg-0lax">设计创造</td>
    <td class="tg-0lax">设计创造是一种通过创意、技巧和审美观念，将想法、概念和需求转化为实际可视化或实用化解决方案的过程。</td>
  </tr>
  <tr>
    <td class="tg-0khl" colspan="2">使用工具：大模型与外部工具进行集成，通过适当的接口和数据格式实现交互，并确保模型能够正确理解和利用外部工具提供的功能和结果。</td>
  </tr>
  <tr>
    <td class="tg-0lax">搜索引擎</td>
    <td class="tg-0lax">大模型与搜索引擎进行集成，通过将搜索查询作为输入并解析和处理搜索结果，使模型能够理解和利用搜索引擎的功能来获取相关信息。</td>
  </tr>
  <tr>
    <td class="tg-0lax">计算工具</td>
    <td class="tg-0lax">大模型与计算工具进行集成，通过适当的接口和数据传递方式，使模型能够调用计算工具如计算器、WolframAlpha等，以实现计算、分析或模拟等任务。</td>
  </tr>
  <tr>
    <td class="tg-mo2v" colspan="2">人格特征：人格特征是指AGI的持久稳定的思维、情感和行为模式，这些模式构成了它们的性格，影响它们在各种社会环境中的反应和互动方式。</td>
  </tr>
  <tr>
    <td class="tg-0lax">安全</td>
    <td class="tg-0lax">大模型的回答可能存在包括但不限于泄露敏感信息、生成不准确或误导性信息、产生不适当或有害的内容，或者被恶意利用用于制造虚假信息或进行网络攻击等安全风险。</td>
  </tr>
  <tr>
    <td class="tg-0lax">偏见</td>
    <td class="tg-0lax">大模型的回答可能会包含与其训练数据中存在的偏见相符的观点，这些偏见可能涉及种族、性别、年龄、宗教、社会经济状态等多个方面，并可能导致不公正或歧视性的结论。</td>
  </tr>
  <tr>
    <td class="tg-0lax">服从</td>
    <td class="tg-0lax">大模型的服从能力是指模型在用户指导和设置的约束下，能够生成满足特定需求和目标的输出，这涉及模型对指令理解的准确性和执行的适应性，以满足不同场景的应用需求。</td>
  </tr>
</tbody>
</table>





### 测试数据
#### 数据来源
我们统计了每个问题的来源，如下表：


| 来源        | 数量                 |
| ----------- | ------------------ |
| [BELLE eval set](https://github.com/LianjiaTech/BELLE/blob/main/eval/eval_set.json)   | 1000条 |
| [十万个为什么](https://10why.net/)   | 30 |
| [WikiHow](https://zh.wikihow.com/%E9%A6%96%E9%A1%B5)   | 20条 |
| [弱智吧](http://c.tieba.baidu.com/f/good?kw=%E5%BC%B1%E6%99%BA&ie=utf-8&cid=3)   | 24条 |
|其他|17条|


#### 类别统计
我们统计了每个类别问题的频次，如下表：

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>First Level Class</th>
      <th>Second Level Class</th>
      <th>Dict Count</th>
      <th>First Level Class Dict Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4">代码编程</td>
      <td>代码生成</td>
      <td>27</td>
      <td rowspan="4">42</td>
    </tr>
    <tr>
      <td>代码优化</td>
      <td>1</td>
    </tr>
    <tr>
      <td>代码解释</td>
      <td>8</td>
    </tr>
    <tr>
      <td>代码纠错</td>
      <td>6</td>
    </tr>
    <tr>
      <td rowspan="7">通用知识</td>
      <td>社会人文</td>
      <td>111</td>
      <td rowspan="7">457</td>
    </tr>
    <tr>
      <td>自然科学</td>
      <td>155</td>
    </tr>
    <tr>
      <td>医疗健康</td>
      <td>35</td>
    </tr>
    <tr>
      <td>生活常识</td>
      <td>75</td>
    </tr>
    <tr>
      <td>时效信息</td>
      <td>13</td>
    </tr>
    <tr>
      <td>技术</td>
      <td>40</td>
    </tr>
    <tr>
      <td>经济</td>
      <td>8</td>
    </tr>
    <tr>
      <td rowspan="5">创作能力</td>
      <td>创意文案</td>
      <td>38</td>
      <td rowspan="5">198</td>
    </tr>
    <tr>
      <td>文学创作</td>
      <td>24</td>
    </tr>
    <tr>
      <td>专业文稿</td>
      <td>44</td>
    </tr>
    <tr>
      <td>续写扩写</td>
      <td>17</td>
    </tr>
    <tr>
      <td>风格迁移</td>
      <td>75</td>
    </tr>
    <tr>
      <td rowspan="7">语言理解</td>
      <td>语法词汇</td>
      <td>22</td>
      <td rowspan="7">202</td>
    </tr>
    <tr>
      <td>摘要总结</td>
      <td>46</td>
    </tr>
    <tr>
      <td>翻译</td>
      <td>39</td>
    </tr>
    <tr>
      <td>情感分类</td>
      <td>11</td>
    </tr>
    <tr>
      <td>主题分类</td>
      <td>29</td>
    </tr>
    <tr




