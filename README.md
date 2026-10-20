# How Scaling Laws Work

**Scaling Laws — 학습하기 전에 loss를 계산한다.** Kaplan et al.(2020)의 「Scaling Laws for Neural Language Models」에 실린 식과 표의 값을 그대로 넣어 브라우저에서 계산해 보는 인터랙티브 교육 자료입니다. loss가 모델 크기 N, 데이터 D, 연산 C의 멱법칙이라 **학습하기 전에 계산할 수 있다**는 것, 그래서 예산 배분도 계산으로 정할 수 있었다는 것, 그리고 그 배분이 2년 뒤 Chinchilla(Hoffmann et al., 2022)에서 어떻게 바뀌었는지를 따라갑니다.

🔗 **[데모 바로가기](https://dev-jonghoonpark.github.io/how-scaling-laws-work/)**

## 다루는 내용

1. **로그-로그 그래프의 직선** · 같은 멱법칙을 보통 축과 로그-로그 축에 그려 보기. N 2배 → loss × 0.95, loss 절반에는 N 약 9,000배
2. **세 개의 멱법칙** · L(N), L(D), L(C_min)(식 1.1~1.3, 표 5). 측정 범위와 외삽 구간, 퍼플렉시티
3. **작은 실험으로 큰 모델 맞히기** · 잡음 섞인 작은 모델 10개로 직선을 맞춰 175B의 loss 외삽. 참 법칙에 바닥(E)이 있으면 외삽이 크게 빗나가는 것까지
4. **크기만 중요하고 모양은 거의 상관없다** · N = 12·n_layer·d², 논문의 실제 모양 (2,128)·(48,1600)·(6,4288)·(207,768), 임베딩 비중(그림 6), “1% loss = 22% 연산”
5. **N과 D를 함께: 과적합의 경계** · L(N,D)(식 1.5, 표 2)로 그림 9 재현, D ≳ 5×10³·N^0.74, 조기 종료 하한(식 5.7)
6. **큰 모델이 더 빨리 배운다** · L(N,S) 학습 곡선(표 3), 임계 배치, 목표 loss에 가장 싸게 닿는 모델 = 수렴값보다 약 10% 위에서 멈추는 모델(식 B.5)
7. **연산량 세기: C ≈ 6ND** · GPT-3·Gopher·MT-NLG·LaMDA·Chinchilla 연산 계산기와 GPU 시간 환산
8. **연산 예산을 어떻게 나눌까** · N ∝ C^0.73, B ∝ C^0.24, S ∝ C^0.03(표 6), 최적 크기에서 벗어날 때의 비용(식 B.16, B.17)
9. **Chinchilla가 바꾼 배분** · 세 방법의 지수 비교(표 2), E + A/N^α + B/D^β의 IsoFLOP 단면, Gopher vs Chinchilla, 파라미터당 20토큰, 결론이 달라진 이유와 방법 3 계수의 재현 문제
10. **멱법칙은 어디서 멈추는가** · L(C_min)과 L(D(C_min))의 교차점(그림 15, 식 6.8)과 지수 민감도, loss ≠ 능력, 데이터 한계
11. **퀴즈** 7문항

## 참고

- Kaplan et al. (2020), *Scaling Laws for Neural Language Models* — [arXiv:2001.08361](https://arxiv.org/abs/2001.08361)
- Hoffmann et al. (2022), *Training Compute-Optimal Large Language Models* — [arXiv:2203.15556](https://arxiv.org/abs/2203.15556)
- Besiroglu et al. (2024), *Chinchilla Scaling: A replication attempt* — [arXiv:2404.10102](https://arxiv.org/abs/2404.10102)

[how-ai-works](https://github.com/dev-jonghoonpark/how-ai-works) 시리즈의 일부입니다.
