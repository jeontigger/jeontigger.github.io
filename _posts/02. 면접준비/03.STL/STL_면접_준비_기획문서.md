# STL 면접 준비 기획문서

## 1. 현재 상태 분석 (analyze_current)

### 1.1 파일 구조 현황

현재 STL 폴더에는 7개의 파일이 있습니다:

- `01.vector.md` - vector 내부 구조
- `02.map_unmap.md` - map vs unordered_map
- `03.set_multiset.md` - set vs multiset
- `05.iterator.md` - iterator 개념
- `06.begin_end.md` - begin/end 동작
- `07.sort_find_remove_erase.md` - 알고리즘 패턴
- `08.erase_remove_idiom.md` - erase-remove idiom

**문제점:**
- 파일 번호가 04번이 누락됨
- 순차적 컨테이너와 연관 컨테이너가 섞여 있음
- 알고리즘 관련 주제가 분산되어 있음

### 1.2 파일별 상세 분석

#### `01.vector.md` - ✅ 양호, 일부 개선 필요

**강점:**
- 사용자 답변과 GPT 답변이 모두 완성됨
- 기본 개념 → 핵심 멤버 → 메모리 할당 → 성능 특성 → 이동/복사 → API → 설계 판단 순서로 잘 구성됨
- 질문의 깊이가 적절함

**개선 필요 사항:**
1. **shrink_to_fit 답변 부재** (사용자 답변: "모르겠습니다")
   - GPT 답변도 불완전: "반드시 줄인다고 보장하지는 않습니다"만 있음
   - 추가 필요: shrink_to_fit의 실제 동작, 언제 사용하는지, 성능 영향

2. **capacity 증가 설명 부정확** (GPT 답변 8번)
   - 현재: "capacity를 여유 있게 늘리기 때문입니다"
   - 수정 필요: "일반적으로 2배씩 증가시키기 때문에 재할당 빈도가 낮아져 평균 O(1)입니다"

3. **사용자 답변의 미세한 오개념**
   - "기존 공간보다 2배 증가한 크기를 새롭게 할당" → 정확하지만 "같은 위치에 복사"는 부정확
   - 새 메모리 블록에 복사/이동하는 것이므로 위치가 달라짐

#### `02.map_unmap.md` - ✅ 양호, 피드백 반영 필요

**강점:**
- 사용자 답변과 GPT 답변이 모두 완성됨
- 기본 개념 → 정렬/순서 → 시간 복잡도 → 해시/비교 → 메모리/성능 → iterator → 실무 판단 순서로 잘 구성됨
- GPT 피드백 섹션이 있어 개선점이 명확함

**개선 필요 사항:**
1. **캐시 친화성 설명 오류** (GPT 피드백 반영 필요)
   - 사용자 답변: "unordered_map이 분기예측적으로 캐시 친화성에서 떨어집니다"
   - GPT 답변: "map은 포인터 기반이라 캐시 효율이 낮고, unordered_map은 상대적으로 낫습니다"
   - GPT 피드백: "map은 노드 단위로 이루어졌기 때문에 캐시 친화성이 오히려 unmap보다 떨어짐"
   - 수정 필요: map은 노드 기반이라 캐시 미스가 많고, unordered_map은 버킷 배열이 연속 메모리라 상대적으로 캐시 효율이 좋음

2. **Iterator 무효화 규칙 설명 부족**
   - 사용자 답변: "map은 요소 하나 이상 erase 되었을 때, unordered_map은 rehashing되었을 때 무효화 됩니다"
   - 더 명확히: map은 erase된 요소의 iterator만 무효화, unordered_map은 rehash 시 모든 iterator 무효화

#### `03.set_multiset.md` - ⚠️ 오개념 수정 필요

**강점:**
- 사용자 답변과 GPT 답변이 모두 완성됨
- 기본 개념 → 중복 허용 → 정렬/탐색 → 사용 사례 → 성능 → iterator/삭제 → 설계 판단 순서로 잘 구성됨
- GPT 피드백 섹션이 있어 개선점이 명확함

**개선 필요 사항:**
1. **multiset 개념 오개념** (사용자 답변 1번)
   - 현재: "multiset은 같은 key를 개수를 카운팅합니다"
   - 수정: "multiset은 같은 key를 중복해서 저장할 수 있습니다"
   - multiset은 카운팅 컨테이너가 아니라 중복 허용 컨테이너임

2. **multiset 사용 사례 오개념** (사용자 답변 2번, 2번)
   - 현재: "개수를 카운팅 하는데 필요하다", "중복된 원소들의 개수를 판단하는데 사용됩니다"
   - 수정: "정렬된 상태에서 중복된 값들을 관리해야 할 때 사용합니다"
   - count()로 개수를 세는 것은 가능하지만, 그게 주 목적은 아님

3. **erase 동작 설명 부정확** (사용자 답변 1번, GPT 피드백)
   - 현재: "multiset은 모든 요소를 삭제합니다"
   - 수정 필요: iterator erase는 하나만, key erase는 해당 키의 모든 인스턴스 삭제
   - GPT 피드백: "iterator erase와 key erase의 존재 구분 필요"

4. **multiset에서 특정 값 하나만 삭제 방법** (사용자 답변: "모르겠습니다")
   - GPT 답변: "iterator를 사용해 하나만 erase합니다"
   - 더 구체적으로: `auto it = ms.find(value); if (it != ms.end()) ms.erase(it);`

#### `05.iterator.md` - ⚠️ GPT 답변 완전히 누락

**강점:**
- 질문 구조가 잘 되어 있음: 기본 개념 → 포인터 관계 → 컨테이너 연계 → 종류 → 알고리즘 연계 → 무효화 → 설계/요약
- 카테고리별로 질문이 체계적으로 구성됨

**문제점:**
1. **GPT 답변 섹션이 비어있음**
   - GPT 답변 섹션에 질문만 반복되어 있고 실제 답변이 없음
   - 모든 질문에 대한 답변 필요

2. **사용자 답변 공간 없음**
   - 다른 파일과 달리 사용자 답변 공간이 제공되지 않음
   - 일관성을 위해 추가 고려

3. **Iterator category별 연산 예시 부족**
   - 질문 21번: "random access iterator가 가능한 컨테이너는 무엇인가요?"
   - 답변에 vector, deque, string 등 구체적 예시 필요

4. **Iterator traits 개념 누락**
   - 고급 주제이지만 면접에서 나올 수 있음
   - 별도 질문 추가 고려

#### `06.begin_end.md` - ✅ 양호

**강점:**
- GPT 답변이 완성되어 있음
- 기본 개념 → 반복 범위 규칙 → 컨테이너별 동작 → const/iterator 종류 → 알고리즘/range-based for → 안전성 → 요약 순서로 잘 구성됨

**개선 필요 사항:**
1. **사용자 답변 공간 없음**
   - 일관성을 위해 추가 고려 (선택사항)

2. **C++20 ranges 개념 언급 부족**
   - 질문 26번에서 range-based for는 다루지만, C++20 ranges 라이브러리는 언급되지 않음
   - 고급 주제이지만 추가 고려 가능

#### `07.sort_find_remove_erase.md` - ✅ 양호

**강점:**
- GPT 답변이 완성되어 있음
- 기본 개념 → sort → find → remove → erase → 컨테이너별 차이 → 실무/버그 포인트 순서로 잘 구성됨
- erase-remove 패턴의 핵심을 잘 다룸

**개선 필요 사항:**
1. **사용자 답변 공간 없음**
   - 일관성을 위해 추가 고려 (선택사항)

2. **컨테이너별 멤버 함수 vs 알고리즘 차이 더 명확히**
   - 질문 1번에서 다루지만, 구체적 예시가 부족
   - 예: list::sort() vs std::sort(), map::find() vs std::find()

#### `08.erase_remove_idiom.md` - ✅ 양호

**강점:**
- GPT 답변이 완성되어 있음
- 기본 개념 → remove 동작 이해 → erase 역할 → 적용 대상 → 변형 패턴 → 성능 → 실무/버그 포인트 순서로 잘 구성됨
- erase-remove idiom의 핵심을 잘 다룸

**개선 필요 사항:**
1. **사용자 답변 공간 없음**
   - 일관성을 위해 추가 고려 (선택사항)

2. **실제 코드 예시 추가 고려**
   - 개념 설명은 충분하지만, 실제 코드 예시가 있으면 더 이해하기 쉬움

### 1.3 전체적인 문제점 요약

1. **일관성 부족**
   - 일부 파일에는 사용자 답변이 있고, 일부는 없음
   - GPT 답변 형식은 대체로 일관되지만, iterator.md는 완전히 비어있음

2. **질문의 깊이 불균형**
   - `vector.md`, `map_unmap.md`, `set_multiset.md`: 상세한 답변이 있으나 일부 오개념 존재
   - `iterator.md`: 답변 섹션이 완전히 비어있음
   - `begin_end.md`, `sort_find_remove_erase.md`, `erase_remove_idiom.md`: GPT 답변은 있으나 사용자 답변 없음

3. **오개념 존재**
   - `vector.md`: capacity 증가 설명 부정확
   - `map_unmap.md`: 캐시 친화성 설명 오류
   - `set_multiset.md`: multiset의 개념과 사용 사례 오개념

---

## 2. 누락된 STL 주제 파악 (identify_missing)

### 2.1 순차 컨테이너 (Sequential Containers)

#### ❌ deque
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - deque의 내부 구조 (청크 기반)
  - vector와 deque의 차이
  - 앞/뒤 삽입 성능 비교
  - 중간 삽입 성능
  - iterator 무효화 규칙
  - 언제 deque를 사용해야 하는가

#### ❌ list / forward_list
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - list의 내부 구조 (이중 연결 리스트)
  - forward_list의 특성 (단일 연결 리스트)
  - list vs vector 성능 비교
  - splice 연산의 의미
  - iterator 무효화 규칙
  - 언제 list를 사용해야 하는가

#### ❌ string
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - string의 내부 구조
  - string vs vector<char> 차이
  - SSO (Small String Optimization)
  - string 연산의 성능 특성
  - c_str()과 data()의 차이
  - string_view (C++17) 언급 가능

### 2.2 연관 컨테이너 (Associative Containers)

#### ✅ map / unordered_map
- **현재 상태**: 완료 (`02.map_unmap.md`)

#### ✅ set / multiset
- **현재 상태**: 완료 (`03.set_multiset.md`)

#### ❌ container_comparison (컨테이너 선택 가이드)
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - 각 컨테이너의 시간 복잡도 비교표
  - 메모리 사용량 비교
  - 캐시 친화성 비교
  - 실무에서 컨테이너 선택 기준
  - 컨테이너 선택 의사결정 트리

### 2.3 컨테이너 어댑터 (Container Adapters)

#### ❌ stack / queue / priority_queue
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - 컨테이너 어댑터 개념
  - 각 어댑터의 내부 컨테이너
  - stack의 사용 사례
  - queue의 사용 사례
  - priority_queue의 동작 방식
  - 커스텀 비교자 사용법

### 2.4 Iterator & 범위

#### ✅ iterator
- **현재 상태**: 완료 (`05.iterator.md`) - 단, GPT 답변 필요

#### ✅ begin/end
- **현재 상태**: 완료 (`06.begin_end.md`)

#### ❌ iterator_invalidation (Iterator 무효화 규칙)
- **현재 상태**: 각 파일에 분산되어 있으나 통합 문서 없음
- **필수 주제**:
  - iterator invalidation 개념
  - 컨테이너별 무효화 규칙 정리표
  - 안전한 순회 방법
  - erase 반환값 활용법
  - 실무에서 자주 발생하는 버그 패턴

### 2.5 STL 알고리즘

#### ✅ sort / find / remove / erase
- **현재 상태**: 완료 (`07.sort_find_remove_erase.md`)

#### ✅ erase-remove idiom
- **현재 상태**: 완료 (`08.erase_remove_idiom.md`)

#### ❌ stl_algorithms (주요 알고리즘 개요)
- **현재 상태**: 일부만 다룸 (sort, find, remove)
- **필수 주제**:
  - 주요 알고리즘 카테고리 (변형/비변형/정렬/이진탐색 등)
  - 알고리즘의 iterator 요구사항
  - 알고리즘과 컨테이너 멤버 함수의 선택 기준
  - 성능 최적화 팁
  - transform, accumulate, count_if 등 주요 알고리즘

### 2.6 고급 주제

#### ❌ functor_lambda (함수 객체와 람다)
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - 함수 객체 (functor) 개념
  - 함수 포인터 vs 함수 객체
  - 람다 표현식 문법
  - 람다 캡처 규칙
  - STL 알고리즘과 람다의 연계
  - std::function 언급

#### ❌ performance_optimization (STL 성능 최적화)
- **현재 상태**: 각 파일에 분산되어 있으나 통합 문서 없음
- **필수 주제**:
  - reserve/resize 최적화
  - 이동 의미론과 STL
  - emplace vs insert
  - 알고리즘 선택 최적화
  - 메모리 할당 최적화
  - 컨테이너 선택 최적화

### 2.7 누락 주제 요약

**우선순위 높음:**
1. deque
2. list / forward_list
3. string
4. container_comparison
5. iterator_invalidation

**우선순위 중간:**
6. stack / queue / priority_queue
7. stl_algorithms
8. functor_lambda

**우선순위 낮음 (고급):**
9. performance_optimization

---

## 3. 재구성된 커리큘럼 구조 (restructure_curriculum)

### 3.1 재구성 원칙

1. **논리적 순서**: 기본 → 심화 → 고급
2. **컨테이너 분류**: 순차 → 연관 → 어댑터
3. **개념 흐름**: 컨테이너 → Iterator → 알고리즘 → 고급 주제
4. **실무 적용**: 각 섹션 마지막에 실무 판단 질문 포함

### 3.2 재구성된 파일 구조

#### Part 1: 기본 컨테이너 (Sequential Containers)

1. `01.vector.md` - vector 내부 구조 및 특성 ✅ (기존 파일)
2. `02.deque.md` - deque vs vector 비교 ❌ (신규)
3. `03.list_forward_list.md` - list와 forward_list ❌ (신규)
4. `04.string.md` - string 컨테이너 특성 ❌ (신규)

**학습 목표:**
- 순차 컨테이너의 내부 구조 이해
- 각 컨테이너의 성능 특성 비교
- 언제 어떤 컨테이너를 사용해야 하는지 판단

#### Part 2: 연관 컨테이너 (Associative Containers)

5. `05.map_unordered_map.md` - map vs unordered_map ✅ (기존 `02.map_unmap.md` 재명명)
6. `06.set_multiset.md` - set vs multiset ✅ (기존 `03.set_multiset.md` 재명명)
7. `07.container_comparison.md` - 컨테이너 선택 가이드 ❌ (신규)

**학습 목표:**
- 연관 컨테이너의 내부 구조 이해
- 정렬된 컨테이너 vs 해시 컨테이너 비교
- 실무에서 컨테이너 선택 기준 마스터

#### Part 3: 컨테이너 어댑터

8. `08.stack_queue_priority_queue.md` - 어댑터 컨테이너 ❌ (신규)

**학습 목표:**
- 컨테이너 어댑터 개념 이해
- 각 어댑터의 사용 사례 파악

#### Part 4: Iterator & 범위

9. `09.iterator.md` - iterator 개념 및 종류 ✅ (기존 `05.iterator.md` 재명명, GPT 답변 필요)
10. `10.begin_end_range.md` - begin/end와 범위 개념 ✅ (기존 `06.begin_end.md` 재명명)

**학습 목표:**
- Iterator 추상화 개념 이해
- Iterator category별 특성 파악
- 범위 기반 프로그래밍 이해

#### Part 5: STL 알고리즘

11. `11.sort_find_remove_erase.md` - 기본 알고리즘 패턴 ✅ (기존 `07.sort_find_remove_erase.md` 재명명)
12. `12.erase_remove_idiom.md` - erase-remove idiom ✅ (기존 `08.erase_remove_idiom.md` 재명명)
13. `13.stl_algorithms.md` - 주요 알고리즘 개요 ❌ (신규)

**학습 목표:**
- STL 알고리즘의 역할 이해
- 알고리즘 vs 컨테이너 멤버 함수 선택 기준
- 주요 알고리즘 패턴 마스터

#### Part 6: 고급 주제

14. `14.functor_lambda.md` - 함수 객체와 람다 ❌ (신규)
15. `15.iterator_invalidation.md` - iterator 무효화 규칙 ❌ (신규)
16. `16.performance_optimization.md` - STL 성능 최적화 ❌ (신규)

**학습 목표:**
- 함수 객체와 람다를 활용한 고급 프로그래밍
- Iterator 무효화로 인한 버그 방지
- STL 성능 최적화 기법 습득

### 3.3 파일 재명명 및 이동 계획

**기존 파일 재명명:**
- `02.map_unmap.md` → `05.map_unordered_map.md`
- `03.set_multiset.md` → `06.set_multiset.md`
- `05.iterator.md` → `09.iterator.md`
- `06.begin_end.md` → `10.begin_end_range.md`
- `07.sort_find_remove_erase.md` → `11.sort_find_remove_erase.md`
- `08.erase_remove_idiom.md` → `12.erase_remove_idiom.md`

**신규 파일 생성:**
- `02.deque.md`
- `03.list_forward_list.md`
- `04.string.md`
- `07.container_comparison.md`
- `08.stack_queue_priority_queue.md`
- `13.stl_algorithms.md`
- `14.functor_lambda.md`
- `15.iterator_invalidation.md`
- `16.performance_optimization.md`

---

## 4. 질문 형식 표준화 (standardize_format)

### 4.1 권장 파일 구조

```markdown
# 🧠 [주제] 면접 질문 리스트

## ✅ [카테고리 1]

1. [질문]
   
   - [사용자 답변 공간] (선택사항)

2. [질문]
   
   - [사용자 답변 공간] (선택사항)

## ✅ [카테고리 2]

...

<details>
<summary>GPT 1줄 답변</summary>
<div markdown="1">

## 📝 모범 답변

### [카테고리 1]

1. [답변]
2. [답변]

### [카테고리 2]

...

</div>
</details>

---

## GPT 피드백

[필요시 피드백 추가]
```

### 4.2 질문 작성 가이드라인

#### 질문 수준
- **기본 개념**: 면접 초반에 나올 수 있는 기본적인 질문
- **심화 개념**: 내부 구조, 동작 원리, 시간 복잡도 등
- **실무 적용**: 언제 사용하는지, 어떤 경우에 선택하는지

#### 질문 순서
1. 기본 개념 질문 (2-3개)
2. 내부 구조/동작 원리 질문 (3-5개)
3. 시간/공간 복잡도 질문 (2-3개)
4. 다른 컨테이너와의 비교 질문 (2-4개)
5. 실무 적용/선택 기준 질문 (1-2개)
6. iterator 무효화 관련 질문 (해당되는 경우, 1-2개)
7. 요약 질문 (1개)

#### 필수 포함 질문 유형
- [ ] 기본 개념 질문 포함
- [ ] 내부 구조/동작 원리 질문 포함
- [ ] 시간/공간 복잡도 질문 포함
- [ ] 다른 컨테이너와의 비교 질문 포함
- [ ] 실무 적용/선택 기준 질문 포함
- [ ] iterator 무효화 관련 질문 포함 (해당되는 경우)
- [ ] 요약 질문 포함

### 4.3 답변 작성 가이드라인

#### GPT 답변 형식
- **1줄 답변**: 간결하고 핵심만 담은 답변
- **카테고리별 구분**: 질문 카테고리와 동일하게 구성
- **번호 매칭**: 질문 번호와 답변 번호 일치

#### 답변 내용 기준
- **정확성**: 기술적으로 정확한 정보 제공
- **간결성**: 면접에서 답변할 수 있을 정도로 간결
- **완전성**: 질문의 핵심을 모두 다룸
- **예시 포함**: 필요시 코드 예시나 구체적 예시 포함

#### 사용자 답변 공간
- **선택사항**: 모든 질문에 필수는 아님
- **일관성**: 파일 내에서 일관되게 적용
- **형식**: 4칸 들여쓰기로 답변 공간 제공

### 4.4 카테고리 명명 규칙

**표준 카테고리:**
- `## ✅ 기본 개념`
- `## ✅ 내부 구조` (또는 `## ✅ 핵심 멤버 요소`)
- `## ✅ 메모리 할당 / 재할당` (해당되는 경우)
- `## ✅ 성능 특성`
- `## ✅ 시간 복잡도`
- `## ✅ iterator / 안정성` (해당되는 경우)
- `## ✅ 실무 / 설계 판단`
- `## ✅ 요약 질문`

**주제별 추가 카테고리:**
- 정렬/순서 관련: `## ✅ 정렬 / 순서`
- 비교 관련: `## ✅ 비교 연산`
- 삭제 관련: `## ✅ 삭제 동작`
- 알고리즘 관련: `## ✅ [알고리즘명] 패턴`

### 4.5 코드 예시 가이드라인

**코드 예시가 필요한 경우:**
- erase-remove idiom 같은 패턴
- iterator 사용법
- 람다 표현식
- 복잡한 알고리즘 사용법

**코드 예시 형식:**
```cpp
// 간단한 설명
std::vector<int> vec = {1, 2, 3, 4, 5};
vec.erase(std::remove(vec.begin(), vec.end(), 3), vec.end());
```

---

## 5. 실행 계획

### Phase 1: 기존 파일 개선 (우선순위: 높음)

1. **파일 번호 재정렬**
   - `02.map_unmap.md` → `05.map_unordered_map.md`
   - `03.set_multiset.md` → `06.set_multiset.md`
   - `05.iterator.md` → `09.iterator.md`
   - `06.begin_end.md` → `10.begin_end_range.md`
   - `07.sort_find_remove_erase.md` → `11.sort_find_remove_erase.md`
   - `08.erase_remove_idiom.md` → `12.erase_remove_idiom.md`

2. **각 파일의 GPT 답변 섹션 완성**
   - `09.iterator.md`: 모든 질문에 대한 GPT 답변 작성

3. **오개념 수정 및 피드백 반영**
   - `01.vector.md`: capacity 증가 설명 수정, shrink_to_fit 답변 보완
   - `05.map_unordered_map.md`: 캐시 친화성 설명 수정
   - `06.set_multiset.md`: multiset 개념 오개념 수정, erase 동작 명확화

4. **질문 형식 표준화**
   - 모든 파일에 동일한 형식 적용
   - 사용자 답변 공간 일관성 확보 (선택사항)

### Phase 2: 신규 파일 생성 (우선순위: 높음 → 중간)

**우선순위 높음:**
1. `02.deque.md` - deque 내부 구조 및 vector 비교
2. `03.list_forward_list.md` - list와 forward_list
3. `04.string.md` - string 컨테이너 특성
4. `07.container_comparison.md` - 컨테이너 선택 가이드
5. `15.iterator_invalidation.md` - iterator 무효화 규칙

**우선순위 중간:**
6. `08.stack_queue_priority_queue.md` - 어댑터 컨테이너
7. `13.stl_algorithms.md` - 주요 알고리즘 개요
8. `14.functor_lambda.md` - 함수 객체와 람다

**우선순위 낮음:**
9. `16.performance_optimization.md` - STL 성능 최적화

### Phase 3: 전체 검토

1. **모든 파일의 질문 품질 검토**
   - 각 파일이 체크리스트를 만족하는지 확인
   - 질문의 깊이가 적절한지 확인

2. **중복 질문 제거**
   - 여러 파일에 걸쳐 중복된 질문 확인 및 정리

3. **누락된 핵심 질문 추가**
   - 각 주제별로 면접에서 나올 수 있는 핵심 질문 확인

4. **최종 정리**
   - 파일명 일관성 확인
   - 형식 일관성 확인
   - 내용 정확성 최종 검토

---

## 6. 체크리스트

각 파일마다 다음을 확인:

### 필수 체크리스트
- [ ] 기본 개념 질문 포함
- [ ] 내부 구조/동작 원리 질문 포함
- [ ] 시간/공간 복잡도 질문 포함
- [ ] 다른 컨테이너와의 비교 질문 포함 (해당되는 경우)
- [ ] 실무 적용/선택 기준 질문 포함
- [ ] iterator 무효화 관련 질문 포함 (해당되는 경우)
- [ ] GPT 답변 섹션 완성
- [ ] 요약 질문 포함

### 선택 체크리스트
- [ ] 사용자 답변 공간 제공 (일관성 유지)
- [ ] 코드 예시 포함 (필요한 경우)
- [ ] GPT 피드백 섹션 포함 (오개념이 있는 경우)

### 형식 체크리스트
- [ ] 파일명이 `##.주제명.md` 형식인가?
- [ ] 제목이 `# 🧠 [주제] 면접 질문 리스트` 형식인가?
- [ ] 카테고리가 `## ✅ [카테고리명]` 형식인가?
- [ ] GPT 답변 섹션이 `<details>` 태그로 감싸져 있는가?
- [ ] GPT 답변이 카테고리별로 구분되어 있는가?

---

## 7. 참고 사항

### 파일명 규칙
- 형식: `##.주제명.md` (##는 2자리 숫자)
- 예시: `01.vector.md`, `05.map_unordered_map.md`

### 마크다운 형식
- 제목: `# 🧠 [주제] 면접 질문 리스트`
- 카테고리: `## ✅ [카테고리명]`
- 질문: 번호와 함께 작성
- 사용자 답변: 4칸 들여쓰기
- GPT 답변: `<details>` 태그 내부에 작성

### 질문 작성 시 주의사항
- 면접에서 실제로 나올 수 있는 수준으로 작성
- 기본 개념부터 심화 개념까지 단계적으로 구성
- 시간 복잡도 관련 질문은 반드시 포함
- 컨테이너 비교 질문은 구체적인 사용 사례 포함

---

**문서 작성일**: 2026-01-09  
**최종 수정일**: 2026-01-09  
**버전**: 1.0
