# 한국어 자연어 → Bash 명령어 생성 모델

이 프로젝트는 **한국어로 작성된 자연어 명령문**을 입력받아, 해당 요청에 대응하는 **Bash 명령어를 한 줄로 생성**하는 인공지능 모델을 만드는 것을 목표로 합니다.

## 주요 기능
- 한국어 → Bash 명령어 자동 매핑
- 의미 기반 평가 시스템 구축
- Hugging Face Transformers + PEFT(QLoRA) 기반 모델 파인튜닝

---

## 데이터셋

- **기반 데이터**: [`jiacheng-ye/nl2bash`](https://huggingface.co/datasets/jiacheng-ye/nl2bash)
  - 영어 자연어 지시문과 bash 명령어 쌍으로 구성
- **가공 과정**:
  1. **한국어 번역**: OpenAI API를 이용해 한국어로 데이터 번역
  2. **데이터 증강**: 의미를 유지한 동의어/어순 변경을 통해 텍스트 데이터 증강
  3. **최종 데이터 수량**: 약 16,000 쌍

---

## 모델 구성

- **Base Model**: [`allganize/Llama-3-Alpha-Ko-8B-Instruct`](https://huggingface.co/allganize/Llama-3-Alpha-Ko-8B-Instruct)
  - 한국어로 사전학습된 LLaMA 3 기반 모델
- **Fine-tuning**: QLoRA 적용 (VRAM 절약 + 빠른 학습)

---

## 파이프라인

1. **한국어 데이터 생성 및 증강**
2. **QLoRA 기반 파인튜닝 (RunPod 사용)**
3. **OpenAI API 기반 의미 유사도 평가 자동화**
4. **정확도 측정 및 모델 개선 반복**
