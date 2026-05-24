# Ai-prompt for learning

本项目是AI辅学的提示词，核心要点在于让AI学会提问，适应用户的学习进度，并且提供个性化的总结。本项目针对以下AI工具做了适配

### Claude desktop

> 使用方式，复制相应文件，然后重命名为CLAUDE.md到相应的文件夹中

**exercises(claude_desktop).md**用于完成题目，但是自己没有掌握好相应知识时。

**course_auto(claude_desktop).md**用于在用户提供课程语音稿与PPT，然后希望用AI当补课老师时。

缺点: 此模式经常会遇到claude仅仅在开头阅读一遍课程内容,后续不再阅读，在记忆中出现混乱，导致后续出现幻觉，虚构课程内容的问题。(可以通过增加hook等强制约束来解决这一问题，这需要后续开发)。 

优点: 这种思路下，claude主动讲解，会给公式等必要的补充，如果是从头学起还是推荐这个

评价: 说对照着语音稿看看，大致知道AI是否偏离事实，还是可以采用这个提示词。

**course_manual(claude_desktop).md**:用于在用户提供课程语音稿与PPT，然后希望自己阅读PPT与语音稿补课时。这个交互方式是，用户自己提问然后AI查找资料，给出循序渐进的引导。

优点: 这样AI出现幻觉的概率小一点

缺点: 需要自己对比语音稿与PPT，对照麻烦，并且语音稿有时候可读性不是很高。

评价:如果用户对课程内容比较熟悉，仅仅是希望提意见问题，可以用这个提示词。

推荐的claude系统提示词是(系统提示词是在UI中放进去的，每次claude对话前都会看，而CLAUDE.md不会自动被claude Desktop阅读，需要我们引导)

```
If i ask you about a file, but you couldn't find it, you should load tools, and read in my directory(/Users/nickname/Desktop/claude_home). If this is a Desktop app, and if claude is teaching user about the course, claude need to read the original course files before every reply.
```

### 设计思路

- 一次性给AI提出太多要求AI容易混乱，并且导致进一步幻觉。因此，我尽可能把不同模式的任务分开成为不同文件，同时，按照时间顺序给出尽可能简明的指令。
- 让AI学会提问，依据用户的水平讲解，而不是一次性全部倒出来
- 提供个性化的总结文件，便于后续的复习整理等。