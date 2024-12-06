입력:
- \(K\): 최적 집합의 크기
- \(S\): 배치 크기
- \(M\): 최적 집합 업데이트 시 생성 샘플의 크기
- \(MAXFEs\): 함수 평가의 최대 허용 횟수
- \(\Omega\): 탐색 공간의 범위
- \(GANIter\): GAN 학습 반복 횟수
- \(DIter\): 판별자 학습 반복 횟수

초기화:
- \(x_{\text{opt}} = \{x^{(1)}, x^{(2)}, ..., x^{(K)} \mid x^{(s)} \sim U(\Omega)\}\), \(s = 1, 2, ..., K\)
- \(MaxEpoch = \lceil \frac{MAXFEs - K}{M} \rceil\)

생성자 사전 학습 (Generator Pre-training):
- \(G\)와 \(D_R\)를 \(U(\Omega)\)를 이용해 식 (8)과 (5)를 사용하여 학습

분포 재조정 (Distribution Reshaping):
- \(epoch = 1\)에서 \(MaxEpoch\)까지 반복:
  - \(iter_G = 1\)에서 \(GANIter\)까지 반복:
    - \(iter_D = 1\)에서 \(DIter\)까지 반복:
      - \(D_I\)를 \(x_{\text{opt}}\)와 식 (4)로 학습
      - \(D_R\)를 \(U(\Omega)\)와 식 (5)로 학습
    - 끝
    - \(G\)를 식 (6)으로 학습
  - 끝
  - \(x_G = G(\eta)\)
  - \(B = x_{\text{opt}} \cup x_G\)
  - \(B\)를 \(f(B)\)의 오름차순으로 정렬
  - \(x_{\text{opt}} = B[:K]\)
  - 식 (7)을 사용하여 \(x_{\text{opt}}\)의 분포 축소
- 끝

출력: \(\arg\min f(x_{\text{opt}})\)
