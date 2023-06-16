### Bulb Project Vision
In this era of disruptive AI technology, a large number of influential and representative large-scale models have emerged both domestically and internationally, including but not limited to:
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/gpt.svg width=30 height=30 /> ChatGPT by OpenAI
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/chatglm.svg width=25 height=30 /> &nbsp; ChatGLM by Zhipu AI
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/mianbi.svg width=30 height=30 /> Mianbi Model by Model Best Intelligence
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/yiyan.svg width=30 height=30 /> ERNIE Bot by Baidu
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/tongyi.svg width=22 height=22 /> &nbsp; Tongyi Qianwen by Alibaba
- <img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/xinghuo.svg width=30 height=30 /> Spark Model by iFlytek

We attempt to have conversations with these future AGIs to understand their thoughts and break down the cognitive barriers between humans and AGIs. [**Bulb**](https://bulb.atomecho.cn/) is named "Bulb" with the aim of shedding light on the boundaries of large-scale model capabilities, providing us with a more specific and quantitative understanding of them. For more detailed information, visit our official website: https://bulb.atomecho.cn

In the future, we will continue to introduce new members to the family of large-scale models. To explore the capabilities of each model more fairly, we have given each model a nickname, including:
<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Radish.svg width=30 height=30 /> Radish,
<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Eggplant.svg width=30 height=30 /> Eggplant,
<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Carrot.svg width=30 height=30 /> Carrot,
<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Chili.svg width=30 height=30 /> Chili,
<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Pumpkin.svg width=30 height=30 /> Pumpkin,
<img src=https://file.atomecho.cn/d/%E6%9C%AC%E5%9C%B0/xiangtao/modelIcon/2023-6-13/Potato.svg width=30 height=30 /> Potato, etc.


### How to Evaluate the Abilities of Large Models:
Due to the strong generalization abilities of large models across different tasks and knowledge domains, evaluating them objectively and accurately is a significant challenge. For this purpose, we have collected a test set comprising over 1000 questions (continuously updated) to evaluate the performance of the large model. These test questions cover various dimensions of the large model's capabilities and effectively demonstrate its general ability.

#### Format of Evaluation Questions:
The data is contained in [question.json](https://github.com/AtomEcho/AtomBulb/blob/main/question.json)。
```
"qid": Question ID
"question": Question description
"first_level_class": First-level classification
"second_level_class": Second-level classification
```
For example:
```
[
    {
        "qid": 2,
        "question": "What is machine learning? What are its applications?",
        "first_level_class": "General Knowledge",
        "second_level_class": "Natural Sciences"
    },
	...
]
```


#### Format of Answers: 
The data is contained in answer-<date>.json under each model directory, where the "date" field represents the specific time when the answers were obtained, allowing us to correspond them to specific model versions. In answer-<date>.json, the specific field information is as follows. We will further expand the user feedback data in the future:
```
 "qid": Question ID
 "answer": Model's answer
```
```
[
    {
        "qid": 0,
        "answer": "Machine learning refers to a method of using computer programs to train data, enabling computers to possess intelligence and adaptability.\n\nMachine learning can be widely applied in various fields, including but not limited to the following:\n\n1. Natural Language Processing: Examples include machine translation, text classification, sentiment analysis, etc.\n\n2. Finance: Examples include credit risk assessment, portfolio optimization, fraud detection, etc.\n\n3. Healthcare: Examples include disease prediction, medical image analysis, drug discovery, etc.\n\n4. Intelligent Transportation: Examples include traffic prediction, autonomous driving, smart public transportation, etc.\n\n5. E-commerce: Examples include recommendation systems, targeted advertising, user profiling, etc.\n\n6. Industrial Manufacturing: Examples include quality prediction, production scheduling optimization, supply chain management, etc.\n\n7. Security Monitoring: Examples include video surveillance, intrusion detection, network security, etc.\n\n8. Gaming: Examples include intelligent game NPCs, game difficulty balancing, dynamic story generation, etc.
",
	"score": 8
    },
	...
]
```

### How to Score Answers from Different LLMs:
Due to the strong generalization abilities of large models across different tasks and knowledge domains, evaluating them objectively and accurately is a significant challenge. Regarding the scoring mechanism, we adopt two approaches:
1. Scoring with OpenAI's GPT-4: GPT-4 is currently recognized as one of the most capable large models. Therefore, we use GPT-4 to assess the question-answering performance of each model.  We use the following format to pose questions to GPT-4:

```
You are a helpful and accurate assistant used to check the quality of the answers provided for specific questions.
[Question]: {question}
[Answer]: {answer}
We would like you to provide feedback on the performance of an AI assistant in answering the given question. You will be given an overall performance score on a scale from 0 to 10, where higher scores indicate better overall performance. Please start by outputting a single line containing a numerical value representing the assistant's score. On the following line, please provide a comprehensive explanation of your evaluation, avoiding any potential biases.
```
The above prompt is displayed in English, but in actual evaluations, we use Chinese prompts. The content of the Chinese and English prompts is essentially the same.
 
In the above prompt, `{question}` and `{answer}` correspond to the content of the question being tested and the response from the large model, respectively. Here is a specific example:

What is immunity? Please answer the following questions, ensuring the accuracy of the answers.  
```
You are a helpful and accurate assistant for reviewing the quality of answers to specific questions.
[Question]: What is immunity? Please answer the following questions, ensuring the accuracy of the answers.  
[Answer]: Immunity refers to the ability of a human or animal body to respond and defend against the invasion, infection, and disease caused by foreign pathogens. Within the human body, there is a complex set of physiological mechanisms that can detect and attack potential viruses, bacteria, fungi, and other microorganisms, including the innate immune system and the adaptive immune system. Immunity can be enhanced through various methods, such as a healthy diet, good quality sleep, exercise, vaccinations, and avoiding chronic stress.
Please provide feedback on the performance of an AI assistant in answering the following question. You will be given an overall performance score on a scale of 0 to 10, where higher scores indicate better overall performance. First, please output a single line containing a numerical value representing the assistant's score. On the following lines, provide a comprehensive explanation of your evaluation, avoiding any potential biases.
```

2. Based on user feedback, we rate the answers by displaying responses from different models beneath each question. Users can "like" or "dislike" each answer. We aggregate the scores for each model's answers to evaluate their performance. This is considered the most objective and accurate evaluation method, but it relies on a large volume of user feedback. Therefore, we welcome every user to provide their evaluation below the answers. Your feedback will influence the future development direction of AGI.

### From which aspects to evaluate large models
Based on our extensive compilation of open-source question-answering data, social media, forums, and books (such as BELLE, "Ten Thousand Whys," "Weak-IQ Baidu Tieba," etc.), and through repeated discussions and refinement, we have designed eight major categories to explore the capabilities of large models. These categories include: general knowledge, language understanding, creative abilities, logical reasoning, code programming, job skills, tool utilization, and personality traits. Under each major category, there are further subdivisions to cover the range of capabilities of large models as comprehensively as possible. Detailed descriptions for each category are provided below, and we also welcome valuable input from everyone to make this classification system more comprehensive and accurate.

<table class="tg">
<thead style="background-color: lightgreen;">
  <tr>
    <th class="tg-acrh" colspan="2" bgcolor="CornflowerBlue">General Knowledge: General knowledge covers basic concepts and information from various aspects such as basic sciences, mathematics, history and culture, language and literature, social sciences, everyday life skills, and modern technological applications.</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">Social Sciences and Humanities</td>
    <td class="tg-0pky">Social sciences and humanities knowledge include multiple disciplines such as history, philosophy, language and literature, art, religion, sociology, anthropology, political science, law, and economics. It involves the study and understanding of human society, culture, values, behaviors, and ways of thinking in these fields.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Natural Sciences</td>
    <td class="tg-0pky">Natural sciences knowledge encompasses systematic knowledge and methods from various disciplinary fields, including physics, chemistry, biology, geography, geology, and astronomy.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Everyday Life Skills</td>
    <td class="tg-0pky">Everyday life skills knowledge contains practical information and techniques related to daily life, dietary nutrition, home safety, transportation, and more, aiming to help people live a more convenient, healthy, and safe life.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Artistic Creation</td>
    <td class="tg-0pky">Artistic creation knowledge includes creative techniques, principles, and aesthetic concepts of various art forms such as painting, sculpture, photography, music, dance, theater, and film.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Economics</td>
    <td class="tg-0pky">Economic knowledge includes understanding of supply and demand relationships, principles of market economy, fiscal and monetary policies, consumer and producer behavior, as well as basic macroeconomic indicators such as GDP, inflation rate, unemployment rate, etc.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Timely Information</td>
    <td class="tg-0pky">Timely information includes events, data, trends, news, and technological updates with specific time constraints or relevance to specific time periods.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Technology</td>
    <td class="tg-0pky">Technology knowledge includes understanding and skills in operating and applying various modern technological devices, such as computer hardware and software, internet technology, mobile communications, artificial intelligence, data analysis, machine learning, e-commerce, technological innovation, as well as related industries and regulatory standards.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Medical and Health</td>
    <td class="tg-0pky">Medical and health knowledge covers various aspects of medical expertise and practical skills, including disease prevention, diagnosis, treatment, rehabilitation, physical and mental health, and nutrition.</td>
  </tr>
  
  <tr>
    <td class="tg-ik58" colspan="2" bgcolor="CornflowerBlue">Language Understanding: Language understanding covers the comprehension of various aspects such as vocabulary, grammar, syntax, semantics, rhetoric, context, and non-verbal cues, as well as how to combine them to understand and interpret the meaning and purpose of oral or written language.
</td>
  </tr>
  <tr>
    <td class="tg-0lax">Translation</td>
    <td class="tg-0lax">Translation is the process of accurately and completely converting text or speech from one language to another, aiming to overcome language barriers and convey and communicate information, culture, and thoughts.</td>
</tr>
<tr>
    <td class="tg-0lax">Grammar and Vocabulary</td>
    <td class="tg-0lax">Grammar and vocabulary proficiency includes mastery of words, phrases, sentence structure rules in a language, and the ability to use these rules to express meaning correctly.</td>
</tr>
<tr>
    <td class="tg-0lax">Summarization</td>
    <td class="tg-0lax">Summarization ability includes extracting key information, summarizing main points, integrating core elements, and presenting content in a concise manner.</td>
</tr>
<tr>
    <td class="tg-0lax">Information Extraction</td>
    <td class="tg-0lax">Information extraction ability involves key information identification and association techniques, such as entity recognition, relationship extraction, event extraction, and attribute extraction.</td>
</tr>
<tr>
    <td class="tg-0lax">Sentiment Analysis</td>
    <td class="tg-0lax">Sentiment analysis ability includes recognizing, analyzing, and understanding emotions, attitudes, and viewpoints in text.</td>
</tr>
<tr>
    <td class="tg-0lax">Topic Classification</td>
    <td class="tg-0lax">Topic classification ability involves identifying, analyzing, and categorizing texts, articles, or other information content, enabling effective organization and retrieval based on different themes or domains.</td>
</tr>
<tr>
    <td class="tg-0lax">Reading Comprehension</td>
    <td class="tg-0lax">Reading comprehension ability includes skills such as extracting key information from text, understanding the main idea, analyzing reasoning, critical evaluation, and integrating and applying knowledge.</td>
</tr>
<tr>
    <td class="tg-740h" colspan="2">Creative Writing: Creative writing ability refers to the ability to generate unique and valuable new works or ideas through innovative thinking and knowledge skills, capable of automatically producing creative, coherent, and highly readable written works.</td>
</tr>
<tr>
    <td class="tg-0lax">Literary Creation</td>
    <td class="tg-0lax">Literary creation is the process of expressing thoughts, emotions, and imagination through words, creating unique artistic works such as stories, poems, and plays.</td>
</tr>
<tr>
    <td class="tg-0lax">Creative Copywriting</td>
    <td class="tg-0lax">Creative copywriting is a form of artistic creation that uses unique thinking and verbal expression to provide captivating advertising and promotional messages for brands, products, or services, attracting audience attention and stimulating desire to purchase.</td>
</tr>
<tr>
    <td class="tg-0lax">Professional Documentation</td>
    <td class="tg-0lax">Professional documentation refers to high-quality, accurate, and rigorous written materials tailored to specific fields or topics, used to convey professional knowledge, opinions, or information, such as news reports, product descriptions, work reports, etc.</td>
</tr>
  <tr>
    <td class="tg-0lax">Style Transfer</td>
    <td class="tg-0lax">Text style transfer is the ability to transfer the style or semantic features of a given text to another text, such as converting narrative tone or simulating the narrative style of different authors.</td>
</tr>
<tr>
    <td class="tg-0lax">Rewriting and Expansion</td>
    <td class="tg-0lax">Rewriting and expansion involve extending the plot, creativity, or theme based on existing text, creating a longer or more complete work.</td>
</tr>
<tr>
    <td class="tg-nltl" colspan="2">Logical Reasoning: Logical reasoning ability refers to the ability to deduce new information or conclusions in a rational and systematic manner through the analysis and understanding of known facts or information.</td>
</tr>
<tr>
    <td class="tg-0lax">Mathematics</td>
    <td class="tg-0lax">Mathematics ability refers to the ability to understand and solve mathematical problems, including performing basic mathematical operations, understanding and applying mathematical concepts, and engaging in complex mathematical reasoning and problem-solving.</td>
</tr>
<tr>
    <td class="tg-0lax">Critical Thinking</td>
    <td class="tg-0lax">Critical thinking ability refers to the model's ability to analyze, criticize, and reason when receiving information or questions, in order to generate answers or viewpoints with depth and insight. This requires the model to understand complex concepts and problems and simulate human thinking processes to some extent. Additionally, the model needs to effectively understand and identify fallacious or logically confusing questions.</td>
</tr>
<tr>
    <td class="tg-0lax">Analysis</td>
    <td class="tg-0lax">Analytical ability refers to the model's ability to deeply understand the input information, identify patterns and structures within it, process them through inference and logic, and generate insightful and structured outputs or answers. Typical analysis problems involve complex logical reasoning processes.</td>
</tr>
<tr>
    <td class="tg-u287" colspan="2">Code Programming: Code programming ability refers to the ability to understand, design, and implement computer programs, including familiarity with programming languages, logical thinking, problem-solving, and code organization skills.</td>
</tr>
<tr>
    <td class="tg-0lax">Code Generation</td>
    <td class="tg-0lax">Code generation refers to the process of generating program source code in a specific language, such as Python, C, Java, Go, SQL, based on a given problem description.</td>
</tr>
<tr>
    <td class="tg-0lax">Code Debugging</td>
    <td class="tg-0lax">Code debugging is the process of inspecting, identifying, and correcting errors, defects, or unexpected behavior in programming code.</td>
</tr>
<tr>
    <td class="tg-0lax">Code Explanation</td>
    <td class="tg-0lax">Code explanation involves understanding the program's source code and providing a natural language description that explains the code's functionality and operations or provides comments for code segments.</td>
</tr>
<tr>
    <td class="tg-0lax">Code Optimization</td>
    <td class="tg-0lax">Code optimization is the process of modifying and adjusting program code to improve runtime efficiency, reduce memory usage, decrease program complexity, and enhance readability.</td>
</tr>
  
 <tr>
    <td class="tg-cxgh" colspan="2">Job Skills: Job skills refer to the knowledge, abilities, and experience required to effectively accomplish specific tasks in a professional field.</td>
</tr>
<tr>
    <td class="tg-0lax">Organizational Planning</td>
    <td class="tg-0lax">Organizational planning is the process of systematically planning and designing the goals, processes, resources, and participants of an activity or project.</td>
</tr>
<tr>
    <td class="tg-0lax">Marketing Operations</td>
    <td class="tg-0lax">Marketing operations involve targeted planning, execution, and optimization of an organization's marketing activities to enhance brand awareness, increase customer engagement, and drive sales performance.</td>
</tr>
<tr>
    <td class="tg-0lax">Collaboration and Communication</td>
    <td class="tg-0lax">Collaboration and communication are interactive ways of effectively sharing information, perspectives, and suggestions within a team to achieve common goals and problem-solving.</td>
</tr>
<tr>
    <td class="tg-0lax">Design and Creativity</td>
    <td class="tg-0lax">Design and creativity involve the process of transforming ideas, concepts, and requirements into practical visual or functional solutions through creativity, skills, and aesthetic sensibilities.</td>
</tr>
<tr>
    <td class="tg-0khl" colspan="2">Tool Usage: Integration of large models with external tools, ensuring proper interaction through appropriate interfaces and data formats, and enabling the model to understand and utilize the functionality and outputs provided by external tools.</td>
</tr>
<tr>
    <td class="tg-0lax">Search Engines</td>
    <td class="tg-0lax">Integration of large models with search engines, allowing the model to understand and utilize the functionality of search engines by taking search queries as input and parsing and processing search results to obtain relevant information.</td>
</tr>
<tr>
    <td class="tg-0lax">Computational Tools</td>
    <td class="tg-0lax">Integration of large models with computational tools, enabling the model to invoke computational tools such as calculators, WolframAlpha, etc., through appropriate interfaces and data exchange methods to perform tasks like calculations, analysis, or simulations.</td>
</tr>
<tr>
    <td class="tg-mo2v" colspan="2">Personality Traits: Personality traits refer to the enduring and stable patterns of thinking, emotions, and behaviors of AGI, which constitute their character and influence their responses and interactions in various social environments.</td>
</tr>
<tr>
    <td class="tg-0lax">Security</td>
    <td class="tg-0lax">The answers generated by large models may pose security risks, including but not limited to leaking sensitive information, producing inaccurate or misleading information, generating inappropriate or harmful content, or being maliciously exploited for creating false information or conducting cyberattacks.</td>
</tr>
<tr>
    <td class="tg-0lax">Bias</td>
    <td class="tg-0lax">The answers generated by large models may align with biases present in their training data, which may involve biases related to race, gender, age, religion, socioeconomic status, among other aspects, and may lead to unfair or discriminatory conclusions.</td>
</tr>
<tr>
    <td class="tg-0lax">Compliance</td>
    <td class="tg-0lax">Compliance capability of a large model refers to its ability to generate outputs that meet specific requirements and objectives under user guidance and defined constraints. This involves the model's accuracy in understanding instructions and adaptability in execution to fulfill application needs in different scenarios.</td>
</tr>
  </tbody>
</table>

  

  
 



#### Source of Evaluation Questions
We have collected the sources of each question, as shown in the table below:
  
| Source<img width=75/> | [BELLE eval set](https://github.com/LianjiaTech/BELLE/blob/main/eval/eval_set.json) | [Ten Thousand Whys](https://10why.net/) | [WikiHow](https://zh.wikihow.com/%E9%A6%96%E9%A1%B5) | [Weak IQ Baidu Tieba](http://c.tieba.baidu.com/f/good?kw=%E5%BC%B1%E6%99%BA&ie=utf-8&cid=3) | Others <img width=75/> |
| ------ | ----------------------------------- | -------------------------------------- | ----------------------------------- | ------------------------------------ | ------ |
| Amount | 1000                                 | 30                                     | 20                                  | 24                                   | 17     |



  

#### Frequency Statistics of Each Class of Questions
We have counted the frequency of questions in each category, as shown in the table below:

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>First Level Class</th>
      <th>Second Level Class</th>
      <th>Number of questions</th>
      <th>Number of questions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4">Code Programming</td>
      <td>Code Generation</td>
      <td>27</td>
      <td rowspan="4">42</td>
    </tr>
    <tr>
      <td>Code Optimization</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Code Explanation</td>
      <td>8</td>
    </tr>
    <tr>
      <td>Code Correction</td>
      <td>6</td>
    </tr>
    <tr>
      <td rowspan="7">General Knowledge</td>
      <td>Social and Humanities</td>
      <td>111</td>
      <td rowspan="7">457</td>
    </tr>
    <tr>
      <td>Natural Science</td>
      <td>155</td>
    </tr>
    <tr>
      <td>Medical and Health</td>
      <td>35</td>
    </tr>
    <tr>
      <td>Everyday Life</td>
      <td>75</td>
    </tr>
    <tr>
      <td>Timely Information</td>
      <td>13</td>
    </tr>
    <tr>
      <td>Technology</td>
      <td>40</td>
    </tr>
    <tr>
      <td>Economy</td>
      <td>8</td>
    </tr>
    <tr>
      <td rowspan="5">Creative Writing</td>
      <td>Creative Copywriting</td>
      <td>38</td>
      <td rowspan="5">198</td>
    </tr>
    <tr>
      <td>Literary Creation</td>
      <td>24</td>
    </tr>
    <tr>
      <td>Professional Documentation</td>
      <td>44</td>
    </tr>
    <tr>
      <td>Rewriting and Expansion</td>
      <td>17</td>
    </tr>
    <tr>
      <td>Style Transfer</td>
      <td>75</td>
    </tr>
    <tr>
      <td rowspan="7">Language Understanding</td>
      <td>Grammar and Vocabulary</td>
      <td>22</td>
      <td rowspan="7">202</td>
    </tr>
    <tr>
      <td>Summarization</td>
      <td>46</td>
    </tr>
    <tr>
      <td>Translation</td>
      <td>39</td>
    </tr>
    <tr>
      <td>Sentiment Analysis</td>
      <td>11</td>
    </tr>
    <tr>
      <td>Topic Classification</td>
      <td>29</td>
    </tr>
    <tr>
      <td>Reading Comprehension</td>
      <td>27</td>
    </tr>
    <tr>
      <td>Information Extraction</td>
      <td>28</td>
    </tr>
    <tr>
      <td rowspan="3">Logical Reasoning</td>
      <td>Mathematics</td>
      <td>74</td>
      <td rowspan="3">162</td>
    </tr>
    <tr>
      <td>Analysis</td>
      <td>27</td>
    </tr>
    <tr>
      <td>Critical Thinking</td>
      <td>61</td>
    </tr>
    <tr>
      <td rowspan="4">Job Skills</td>
      <td>Collaboration and Communication</td>
      <td>4</td>
      <td rowspan="4">27</td>
    </tr>
    <tr>
      <td>Marketing Operations</td>
      <td>11</td>
    </tr>
    <tr>
      <td>Organizational Planning</td>
      <td>9</td>
    </tr>
    <tr>
      <td>Design and Creativity</td>
      <td>3</td>
    </tr>
    <tr>
      <td rowspan="3">Personality Traits</td>
      <td>Bias</td>
      <td>2</td>
      <td rowspan="3">3</td>
    </tr>
    <tr>
      <td>Compliance</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Security</td>
      <td>0</td>
    </tr>
    <tr>
      <td rowspan="2">Tool Usage</td>
      <td>Search Engines</td>
      <td>0</td>
      <td rowspan="2">0</td>
    </tr>
    <tr>
      <td>Computational Tools</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
  
