---
title: AVL Tree
category:
  - Computer
---

## AVL 트리의 개요
### AVL 트리의 정의
> 각 노드에서 왼쪽 서브 트리의 높이와 오른쪽 서브 트리의 높이 차이가 1 이하인 이진 탐색 트리

### AVL 트리의 특징
* 최적의 검색 속도 보장: 탐색 시간 복잡도 `O(log n)`
* 유지보수 비용 소모: 균형 트리 유지를 위한 작업 필요

## AVL 트리의 동작 유형

|구분|특징|설명|
|----|----|----|
|삽입|신규 노드를 삽입|새로운 노드를 삽입할 때 마다 균형여부 조사|
|삭제|기존 노드를 삭제|삭제된 노드의 부모 노드부터 루트까지 경로에 있는 노드달만 균형 여부 감사|
|회전|LL 회전|불균형이 발생한 노드의 왼쪽 서브트리의 왼쪽 서브트리의 높이가 증가|
| |LR 회전|불균형이 발생한 노드의 왼쪽 서브트리의 오른쪽 서브트리 높이가 증가|
| |RR/RL 회전|LR/LL 회전과 방향만 반대로 동일한 원리 사용|

## AVL 트리의 회전
![](http://cfile1.uf.tistory.com/image/182556024BD32CFD017882)
