# Generation-For-NLP
## 수능형 문제 풀이 모델 생성
본 프로젝트는 '한국어'와 '시험'이라는 주제에 맞춰서 작은 모델들로 수능 시험을 풀어보는 태스크입니다. 

<br><br>

## 1. Overview

## 2. 프로젝트 구성
### ⏰ 개발 기간
- 2024년 11월 11일 ~ 2024년 11월 28일
- 부스트캠프 AI Tech NLP 트랙 13-15주차

<br>

### ✨ 분석 환경
- Upstage AI Stages 제공 NVIDIA V100 GPU Server 활용
- OS : Linux
- Language : Python
- Libraries(mainly used) : Pytorch, Hugging Face, Wandb etc.

<br>

## 3. 수행 내용

### 1️⃣ 기존 Baseline 학습 방식
- 모델에 `System` 및 `User prompt`로 문제를 제시한 뒤, `Assistant prompt`로 정답을 알려주는 **Teacher Forcing** 방법 사용.
- **한계**:
  - Loss 계산이 단일 정답에만 의존하여 Fine-Tuning의 정확도가 낮음.

### 2️⃣ 개선된 Fine-Tuning 방식
- **GPT-4o Mini API**를 활용하여 **정답과 근거**를 함께 생성.
- 모델이 정답과 근거를 모두 출력하도록 학습 데이터 수정.

#### 예시
```text
Q: 다음 내용에 대해 알맞는 것을 고르시오.
<지문>
<선지>
A: 위 내용은 임진왜란에 관련된 내용이므로 3번이 알맞는 선지입니다.

```
### 📚 데이터 증강
KorQuAD 기반 데이터 증강
KorQuAD 1.0의 역사 관련 지문을 추출.
GPT-4o API를 활용하여 데이터를 증강.
Fine-Tuning 결과:
3B 이하 모델: 성능 향상 미미.
8B 이상 모델: 약 3% 성능 향상.

### 🛠️ Corpus 구축 및 RAG 연결
Corpus 구축
KeyBERT를 활용하여 Train 데이터의 Anchor Text 추출.
추출한 키워드와 일치하는 Korean Wiki 문서의 Title 기반으로 Corpus 생성.
RAG 연결
구축한 Corpus를 RAG(Retrieval-Augmented Generation) 방식에 연결.
결과:
성능이 오히려 하락, 추가적인 최적화 필요.


## 4. 결과
### 📊 결과 비교

| **Hard Voting/Model**                     | **Eval_ACC** | **ACC (public)** | **ACC (private)** |
|-------------------------------------------|---------------|------------|--------------|
| **Exaone + Qwen + Llama (Hard Voting)**   | 0.6728        | 0.6437     | -            |
| **LGAI-EXAONE/EXAONE-3.0-7.8B-Instruct**  | 0.5500        | 0.6498     | 0.6253       |
| **MLP-KTLim/llama-3-Korean-Bllossom-8B**  | 0.4800        | 0.6244     | 0.5839       |
| **Qwen 2.5 instruct**                     | 0.6400        | 0.6106     | 0.5816       |
| **meta-llama/Llama-3.2-8B-Instruct**      | 0.4400        | 0.5806     | 0.5655       |
| **CarrotAI/Llama-3.2-Rabbit-Ko-3B-Instruct** | 0.7300      | 0.5668     | 0.5438       |
| **Bllossom/llama-3.2-Korean-Bllossom-3B** | 0.6300        | 0.5392     | 0.5103       |
| **beomi/gemma-ko-2b (Baseline)**          | 0.4900        | 0.4055     | 0.4069       |

---
- 기본적으로 모델의 파라미터 수가 클수록 성능 향상이 있었음
- 같은 방법이라도 작은 모델에서 성능향상이 없는 반면 큰 모델에서 성능향상이 있는 경우가 있었음
- 한국어 모델로는 Baseline에서 모델만 바꿨을 때 Exaone 8B 모델이 가장 좋은 성능을 보였음
## 5. Team
<table>
    <tbody>
        <tr>
            <td align="center">
                <a href="https://github.com/Kimyongari">
                    <img src="https://github.com/Kimyongari.png" width="100px;" alt=""/><br />
                    <sub><b>Kimyongari</b></sub>
                </a><br />
                <sub>김용준</sub>
            </td>
            <td align="center">
                <a href="https://github.com/Soobin-Park">
                    <img src="https://github.com/Soobin-Park.png" width="100px;" alt=""/><br />
                    <sub><b>Soobin-Park</b></sub>
                </a><br />
                <sub>박수빈</sub>
            </td>
            <td align="center">
                <a href="https://github.com/seohyeon0677">
                    <img src="https://github.com/seohyeon0677.png" width="100px;" alt=""/><br />
                    <sub><b>seohyeon0677</b></sub>
                </a><br />
                <sub>이서현</sub>
            </td>
            <td align="center">
                <a href="https://github.com/Aitoast">
                    <img src="https://github.com/Aitoast.png" width="100px;" alt=""/><br />
                    <sub><b>Aitoast</b></sub>
                </a><br />
                <sub>정석현</sub>
            </td>
            <td align="center">
                <a href="https://github.com/uzlnee">
                    <img src="https://github.com/uzlnee.png" width="100px;" alt=""/><br />
                    <sub><b>uzlnee</b></sub>
                </a><br />
                <sub>정유진</sub>
            </td>
        </tr>
    </tbody>
</table>

<br><br>

---

<br>

## 📖 Reference
이 프로젝트는 다음을 참고하여 개발되었습니다:
KorQuAD 1.0 데이터셋
KeyBERT: Minimal Keyword Extraction
Hugging Face Transformers
GPT-4o Mini API Documentation
RAG: Retrieval-Augmented Generation