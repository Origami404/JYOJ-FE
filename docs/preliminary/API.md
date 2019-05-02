# API

母 url: /api/preliminary/
初赛题目按 _"份"(exam)_ 来组织, 每一份中有一道或多道 _"题目"(problem)_.

## 获取题面

url: exam?exam_id=233
method: GET

```json
{
  "exam-name": "exam-name",
  "problems": {
    "choice": [
      {
        "stem": "题面",
        "option": ["选项内容"],
        "mark": 2
      }
    ],
    "mulchioce": [
      {
        "stem": "题面",
        "option": ["选项内容"],
        "mark": 5
      }
    ],
    "program_result": [
      {
        "code": "#include <cstdio>\nusing namespace std;\nint main() {\n\tprintf(\"Hello, World!\");\n\treturn 0;\n}\n",
        "questions": ["题面"],
        "mark": 5
      }
    ],
    "gap_filling": [
      {
        "stem": "题面",
        "mark": 5
      }
    ],
    "program_competion": [
      {
        "code": "#include <cstdio>\nusing namespace std;\nint main() {\n\tprintf(\"$1\");\n\treturn 0;\n}\n",
        "mark": 5
      }
    ]
  }
}
```

`problem`中有四个数组, 含义如下:
|JSON 名称|含义|
|:-----:|:--:|
|choice|单选题|
|mulchoice|多选题|
|gap_filling|填空|
|program_result|看程序写输出|
|program_competion|补全程序|
题目顺序按数组中对象的顺序排列
数组中对象的具体含义见键值, `mark`为分值
选择题中`options`数组第 i 项会被渲染为 i+'A'

## 提交

提交答案
url: exam
method: POST
前端提交的 data:

```json
{
  "exam_id": 2333,
  "answer": {
    "choice": [1, 2],
    "mulchoice": [[1, 2], [2, 4]],
    "gap_filling": ["xxx", "aaa"],
    "program_result": ["xxx", "aaa"],
    "program_competion": [["xxx", "sss"], ["xxx", "sfaf"]]
  }
}
```

后端返回的 data:

```json
{
  "judge_id": "xxxx"
}
```

`judge_id`是一个 UUID, 用于标识提交的答案, 长 xxx 位(未定)

获取判定结果
url: judge_result?judge_id=2334sda2s
method: GET

```json
{
  "result": {
    "choice": [1, 0],
    "mulchoice": [0, 1],
    "gap_filling": [1, 0],
    "program_result": [[1, 0], [0, 1]],
    "program_competion": [[1, 0], [1, 1]]
  }
}
```
