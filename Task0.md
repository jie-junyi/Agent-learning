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

1. 历史信息是刚需。历史信息是唯一能让 agent 无法完整运行的消融项，若无法查看已执行的操作内容，agent 就会无限重复相同动作。

2. 推理可以舍弃。推理的重要性相对有限，思考过程更多用于提升复杂问题的解决准确度，且推导得出的"为什么"可以从上一步的"是什么"内容中还原，移除推理模块几乎不会造成效果分数下降。

3. Tool calling 方面。工具定义与工具结果是产生幻觉的两个源头，二者不会表现为报错，只会输出格式完全合规的错误答案。由于模型没有开展行动验证，仅靠空想生成结果，会产生严重的幻觉问题。

4. no_tool_results 场景下，模型会持续出现误判，本次测试中工具累计调用了 11 次，始终反复执行相同操作，核心原因是模型无法获取工具返回结果，直接干扰了正常决策。
