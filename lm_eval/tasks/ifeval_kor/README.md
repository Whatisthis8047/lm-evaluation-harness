# IFEval-Kor
## IFEval-Kor: 한국어 LLM Instruciton Following 벤치마크
- This is custom branch for IFEval-Kor benchemark, forked from `lm-eval-harness` Benchmark Framework [[Original Repo](https://github.com/EleutherAI/lm-evaluation-harness)]. Transported IFEval Benchmark into Korean.

구글 리서치팀에서 개발한 IF 벤치마크를 한국어에서도 테스트할 수 있도록 한국어용으로 변형한 벤치마크입니다.


## 기존 벤치마크와 차이점:

**"데이터"** 와 **"채점 코드"** 에 대한 변경이 이루어졌습니다.
### 데이터
HF 레포: [whatisthis8047/IFEval-Kor](https://huggingface.co/datasets/whatisthis8047/IFEval-Kor)
google/IFEval 데이터셋을 GPT를 이용하여 번역한 후, 수기로 검수하였습니다.
제거된 항목:
- 번역이 어색하거나, 잘못 되었던 문장
- 서구권 편향적인 질문
- 채점 항목이 알파벳에 종속적인 지시 문항. (예: 대문자로 작성하시오 등)

이외 자세한 전처리 과정은 허깅페이스 데이터셋 카드에 업데이트하도록 하겠습니다.

### 채점 코드 
1. `instruction._CONSTRAINED_RESPONSE_OPTIONS` 번역
2. `instruciton._ENDING_OPTIONS` 번역
3. KeywordChecker, KeywordFrequencyChecker, ParagraphFirstWordCheck, KeySenctenceChecker, ForbiddenWords, RepeatPromptThenAnswer, EndChecker 
   1. unicode.normalize('NFC',)로 정규화 수행
4. `instructions_util.count_sentences()` 수정
   1. nltk 라이브러리(영문 형태소 분석기) 의존성 제거


설치방법 (사용법은 [lm-evaluation-harness 레포](https://github.com/EleutherAI/lm-evaluation-harness) 참고)
```
git clone --depth 1 https://github.com/Whatisthis8047/lm-evaluation-harness.git
cd lm-evaluation-harness
pip install -e .
```

버그나, 개선사항에 대한 피드백은 언제나 환영입니다 :)

이건모 | email: rjsah80471@gmail.com



아래는 원본 IFEval 벤치마크 설명입니다.
---
# IFEval

### Paper

Title: Instruction-Following Evaluation for Large Language Models
Abstract: https://arxiv.org/abs/2311.07911

One core capability of Large Language Models (LLMs) is to follow natural language instructions. However, the evaluation of such abilities is not standardized: Human evaluations are expensive, slow, and not objectively reproducible, while LLM-based auto-evaluation is potentially biased or limited by the ability of the evaluator LLM. To overcome these issues, we introduce Instruction-Following Eval (IFEval) for large language models. IFEval is a straightforward and easy-to-reproduce evaluation benchmark. It focuses on a set of "verifiable instructions" such as "write in more than 400 words" and "mention the keyword of AI at least 3 times". We identified 25 types of those verifiable instructions and constructed around 500 prompts, with each prompt containing one or more verifiable instructions. We show evaluation results of two widely available LLMs on the market. Our code and data can be found at https://github.com/google-research/google-research/tree/master/instruction_following_eval

Homepage: https://github.com/google-research/google-research/tree/master/instruction_following_eval


### Citation

```
@article{zhou2023instructionfollowing,
  title={Instruction-Following Evaluation for Large Language Models},
  author={Jeffrey Zhou and Tianjian Lu and Swaroop Mishra and Siddhartha Brahma and Sujoy Basu and Yi Luan and Denny Zhou and Le Hou},
  journal={arXiv preprint arXiv:2311.07911},
  year={2023},
}
```

### Groups and Tasks

#### Groups

* Not part of a group yet

#### Tasks

* `ifeval`

### Checklist

For adding novel benchmarks/datasets to the library:
* [x] Is the task an existing benchmark in the literature?
  * [x] Have you referenced the original paper that introduced the task?
  * [x] If yes, does the original paper provide a reference implementation? If so, have you checked against the reference implementation and documented how to run such a test?


If other tasks on this dataset are already supported:
* [ ] Is the "Main" variant of this task clearly denoted?
* [ ] Have you provided a short sentence in a README on what each new variant adds / evaluates?
* [ ] Have you noted which, if any, published evaluation setups are matched by this variant?
