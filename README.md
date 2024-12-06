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
📚 데이터 증강
KorQuAD 기반 데이터 증강
KorQuAD 1.0의 역사 관련 지문을 추출.
GPT-4o API를 활용하여 데이터를 증강.
Fine-Tuning 결과:
3B 이하 모델: 성능 향상 미미.
8B 이상 모델: 약 3% 성능 향상.
```

## 4. Team
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

## Reference