---
layout: post
title: "Mechanism Shift During Post-training from Autoregressive to Masked Diffusion Language Models"
date: 2026-01-22
tags: [arxiv, diffusion]
source: arxiv
paper_url: https://arxiv.org/pdf/2601.14758.pdf
code_url: 
---

## Abstract (One-liner)

자동회귀 모델(ARM)을 마스킹 확산 모델(MDM)로 후처리 학습할 때 내부 계산 메커니즘이 작업 구조에 따라 체계적으로 재구성되며, 지역적 의존성 작업에서는 자동회귀 회로를 유지하지만 글로벌 계획 작업에서는 초기층 처리를 강화한 새로운 회로를 형성함을 밝힘.

### Key points
- MDM 후처리는 매개변수 조정이 아닌 내부 계산 구조의 근본적 재구성 유도
- 지역적 인과적 종속성 작업(IOI)에서는 자동회귀 회로를 대부분 유지
- 글로벌 계획 작업(COUNTDOWN)에서는 초기층 활성화 증가와 분산적 통합으로 전환
- MDMs는 단순히 자동회귀 히وري스틱을 재포장하는 것이 아니라 진정한 양방향 추론 메커니즘 습득

---

## Methods

ARM(자동회귀 모델)과 MDM(마스킹 확산 모델) 간 회로 분석을 통해 기전 변화를 비교. Qwen2.5-7B/Llama-2-7B를 기반으로 Dream-Base-7B/DiffuLLaMA-7B로 후처리한 모델을 대상으로 IOI(지역적 인과) 및 COUNTDOWN(글로벌 계획) 작업에서 회로 구조 분석 수행.

### Details
- 모델: Qwen2.5-7B → Dream-Base-7B, LLaMA-2-7B → DiffuLLaMA-7B
- 분석 방법: EAP-IG(Edge Attribution Patching with Integrated Gradients) 기반 회로 발견, Top-K 구성 요소 비교, Logit Lens 및 뉴런 수준 해석
- 데이터셋: IOI(간접 목적어 식별), COUNTDOWN(숫자 연산 계획)
- 학습 설정: IOI(1단계), COUNTDOWN(목표 시퀀스 길이와 동일한 확산 단계)

### Key Equations
- (No key equations)

**Evidence quality:** high

---

## Results

IOI 작업에서는 ARM과 MDM 간 회로 유사도가 높으나 COUNTDOWN 작업에서는 극도로 낮은 유사도를 보여 글로벌 계획 작업에 대한 MDM의 독립적 회로 구조를 확인.

### Benchmarks / Eval
- IOI: 지역적 인과 추론 테스크 (인덕션 헤드 주도)
- COUNTDOWN: 글로벌 계획 테스크 (숫자 계획 및 목표 조건 만족)

### Numbers
- IOI 작업의 엣지 오버랩: 0.193 (Qwen/Dream), 0.088 (LLaMA/DiffuLLaMA)
- COUNTDOWN 작업의 엣지 오버랩: 0.008 (Qwen/Dream), 0.032 (LLaMA/DiffuLLaMA)
- COUNTDOWN 작업에서 MDM의 초기층 활성화 비율: 2배 이상 증가

### Key Equations
- (No key equations)

### Limitations
- IOI와 COUNTDOWN 두 가지 테스크만 분석하여 일반화 제한
- EAP-IG 기반 스파스 회로 발견으로 보조 메커니즘 누락 가능성
- 대규모 모델 분석 시 계산 리소스 한계

**Evidence quality:** high

---

## Takeaways

**Why it matters**  
MDM이 자동회귀 히وري스틱을 재사용하는지 여부를 규명하여, 확산 아키텍처의 이론적 장점(비시퀀셜 글로벌 계획)이 실제로 구현되는지 입증함.

### Who should care
- 언어 모델 개발자
- 기계적 해석 연구자
- 확산 기반 모델 최적화 담당자

### What to try next
- 다양한 추론 작업(예: 복잡한 논리 테스크)으로 기전 변화 확대 분석
- 더 큰 규모의 모델(예: Qwen-72B)에서 동일 프레임워크 적용
- 초기층 활성화 증가가 계산 효율성에 미치는 영향 평가

---

## Links
- Paper/Report: https://arxiv.org/pdf/2601.14758.pdf
- Code: N/A
