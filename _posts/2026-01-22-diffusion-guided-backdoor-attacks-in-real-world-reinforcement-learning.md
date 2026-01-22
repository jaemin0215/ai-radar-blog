---
layout: post
title: "Diffusion-Guided Backdoor Attacks in Real-World Reinforcement Learning"
date: 2026-01-22
tags: [arxiv, diffusion]
source: arxiv
paper_url: https://arxiv.org/pdf/2601.14104.pdf
code_url: 
---

## Abstract (One-liner)

기존 강화학습 백도어 공격이 실제 로봇의 안전 제약 제어 스택으로 인해 약화되는 문제를 해결하기 위해 조건부 확산 모델을 활용한 물리적 패치 트리거 생성 및 이득 기반 포이즌 전략을 제안한 DGBA 프레임워크를 소개한다.

### Key points
- 실제 로봇 배포 시 속도 제한, 충돌 회피 등의 안전 제약 제어 스택이 기존 백도어 공격을 약화시키는 '감쇠' 현상을 규명
- 실제 환경 변동에 강한 물리적 패치 트리거를 조건부 확산 모델로 생성
- 결정적 상태(이득 기반)에만 포이즌 데이터 주입으로 공격 효율성 최적화
- TurtleBot3에서 기존 방법 대비 공격 성공률 83.5% 달성

---

## Methods

실제 로봇 환경에서 효과적인 백도어 공격을 위한 DGBA 프레임워크 제시. 물리적 패치 트리거와 조건부 확산 모델, 이득 기반 포이즌 전략을 결합하여 안전 제약 제어 스택을 우회함.

### Details
- 패치 트리거: 16x16 크기의 바닥용 인쇄 가능한 패치 (저해상도 카메라 입력에 대응)
- 조건부 확산 모델: U-Net 아키텍처, 노이즈 예측 손실(Ldiff), 시나리오별 패치 분포 생성
- 물리 스타일 증강: 무작위 확대, 원근 왜곡, 밝기/대비 변동, 부분 가림 적용
- 이득 기반 포이즌: PPO에서 이득(|At|) 기준 상위 5% 상태만 포이즌 (β=0.05)
- 블랙박스 제어 스택 가정: 실제 로봇 제어 스택(C(·))을 모델링하지 않고 실행 행동 기준 평가

**Evidence quality:** high

---

## Results

TurtleBot3에서 실제 로봇 배포 시 기존 백도어 공격은 감쇠로 인해 실패하지만, DGBA는 고공격 성공률과 정상 작업 성능을 동시에 달성.

### Benchmarks / Eval
- TurtleBot3 Burger 플랫폼 (ROS 네비게이션 스택 포함)
- 정적 장애물 회피 태스크, 목표 도달 성공률 측정
- 실제 환경에서 안전 제약 제어 스택 활성화 상태 하에서 평가

### Numbers
- PPO 범용: 공격 성공률(ASR) 83.5% (BadRL: 57.0%, SleeperNets: 21.3%)
- 정상 작업 성공률(CSR): DGBA 89.1% (Clean PPO: 91.1%)
- TRPO 범용: ASR 76.3% (BadRL: 46.5%)
- 증강 미적용 시 ASR 56.7% → 물리 스타일 증강 필수
- 확산 모델 미적용 시 ASR 43.4% → 패치 분포 생성의 중요성 입증

### Limitations
- 포이즌 비용 증가(β=15%) 시 정상 작업 성능(CSR) 81.6%로 하락
- 확산 모델 학습에 추가 컴퓨팅 리소스 소요
- TurtleBot3에 국한된 평가로 다양한 로봇 아키텍처 일반화 검증 필요

**Evidence quality:** high

---

## Takeaways

**Why it matters**  
실제 로봇 시스템의 안전 제약 제어 스택으로 인해 기존 강화학습 보안 연구가 실용화되지 못하는 문제 해결. 실제 배포 환경에서의 보안 취약점 심층 분석 필수.

### Who should care
- 로봇 시스템 개발자
- 강화학습 보안 연구자
- 실제 적용 기업의 보안 팀
- 안전 제약을 갖춘 자율 시스템 설계자

### What to try next
- 다양한 로봇 플랫폼(예: 산업용 로봇)에서 DGBA 일반화 검증
- 실시간 제어 스택 동역학 모델링을 통한 공격 강도 최적화
- 다중 트리거 패턴 혼합 전략 개발로 더 높은 공격 성공률 달성

---

## Links
- Paper/Report: https://arxiv.org/pdf/2601.14104.pdf
- Code: N/A
