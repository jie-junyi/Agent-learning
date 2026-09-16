# Task0

实验1-1 上下文的关键作用

运行下列代码，进行消融实验，本次模型供应商和模型选择为deepseek-v4.1-flash，即deepseek falsh。

```
python main.py --mode ablation --provider deepseek --cases 3
```

得到以下消融实验结果。

![image-20260916225021847](https://raw.githubusercontent.com/jie-junyi/blog_image/main/picgo20260916225022022.png)

![image-20260916225532858](https://raw.githubusercontent.com/jie-junyi/blog_image/main/picgo20260916225532936.png)

![image-20260916225624535](https://raw.githubusercontent.com/jie-junyi/blog_image/main/picgo20260916225624677.png)

得到结论如下：
1：历史信息是刚需。因为是唯一一个让 agent 彻底跑不完的消融。看不见自己做过什么，就无限重复。

2：推理可以丢。推理并没有那么重要，思考很多时候更是用于解决复杂问题的准度，而且"为什么"能从上一步的"是什么"里恢复，所以移除它几乎不掉分。

3：Tool calling方面。工具定义 + 工具结果才是幻觉的两个源头，而且它们不表现为报错，表现为一个格式完美的错误答案。因为模型没有进行行动验证，只是自己空想出来的结果，会有极大的幻觉。

4：no_tool_results，模型一直进行误判，工具调用了11次，一直反复执行，就是因为拿不到结果，影响模型决策。

