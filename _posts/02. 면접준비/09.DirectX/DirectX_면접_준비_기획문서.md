# DirectX 면접 준비 기획문서

## 1. 현재 상태 분석 (analyze_current)

### 1.1 파일 구조 현황

현재 DirectX 폴더에는 파일이 없습니다:

**상태:** ❌ 완전히 비어있음

**관련 폴더:**
- `08.그래픽스/` - 범용 그래픽스 개념 (렌더링 파이프라인, 셰이더, 좌표계 등)
- `09.DirectX/` - DirectX API 특화 (Direct3D API, 리소스 관리, 버전별 차이 등)

**구분:**
- 그래픽스 폴더: 렌더링 파이프라인, 셰이더 개념, 좌표계 변환 등 범용 그래픽스 이론
- DirectX 폴더: DirectX API 사용법, Device/Context 개념, 리소스 관리, 버전별 차이 등 DirectX 특화 내용

### 1.2 전체적인 문제점 요약

1. **완전히 비어있음**
   - 폴더만 존재하고 파일이 없음
   - DirectX 관련 면접 질문 준비 불가
   - Windows 게임 개발 면접에서 중요한 주제 누락

2. **주제 범위 불명확**
   - DirectX의 핵심 주제가 정의되지 않음
   - 면접에서 나올 수 있는 질문 범위 미정
   - 그래픽스 폴더와의 구분 기준 불명확

3. **그래픽스 폴더와의 관계**
   - 그래픽스 폴더는 범용 개념 중심 (렌더링 파이프라인, 셰이더 등)
   - DirectX 폴더는 API 특화 중심 (Direct3D API, 리소스 관리 등)
   - 두 폴더는 상호 보완적 관계

4. **실무 요구사항 반영 필요**
   - 던전앤파이터 등 Windows 게임 개발에서 DirectX는 필수
   - DirectX에 대한 높은 이해도 요구
   - 그래픽 퀄리티 향상 및 성능 최적화 경험 중요

---

## 2. 누락된 DirectX 주제 파악 (identify_missing)

### 2.1 DirectX 기본 개념

#### ❌ DirectX 기본 개념
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - DirectX란 무엇인가
  - DirectX의 주요 컴포넌트 (Direct3D, DirectX Graphics, DirectSound 등)
  - DirectX의 역할과 목적
  - Windows 게임 개발에서 DirectX 선택 이유
  - DirectX vs OpenGL 비교
  - DirectX의 역사와 발전 과정

### 2.2 DirectX 버전별 차이

#### ❌ DirectX 버전별 차이
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - DirectX 9의 특징과 한계
  - DirectX 11의 주요 변화 (Device Context, Compute Shader 등)
  - DirectX 12의 Low-level API 특징
  - 각 버전의 성능 특성 비교
  - 언제 어떤 버전을 사용하는가
  - 버전별 호환성과 마이그레이션 고려사항

### 2.3 DirectX API 기본

#### ❌ DirectX API 기본
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - Device와 Context 개념
  - Device 생성 과정 (D3D11CreateDevice 등)
  - Swap Chain 생성 및 관리
  - Render Target View (RTV) 생성
  - Depth Stencil View (DSV) 생성
  - Viewport 설정
  - 기본 렌더링 루프 구조

### 2.4 DirectX 리소스 관리

#### ❌ DirectX 리소스 관리
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - Vertex Buffer 생성 및 사용
  - Index Buffer 생성 및 사용
  - Constant Buffer (CBuffer) 개념과 사용법
  - Texture 리소스 생성 및 관리
  - Shader Resource View (SRV) 생성
  - 리소스 생명주기 관리
  - 리소스 해제 및 메모리 관리
  - 리소스 바인딩 (IASetVertexBuffers, PSSetShaderResources 등)

### 2.5 DirectX 렌더링 상태

#### ❌ DirectX 렌더링 상태
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - Rasterizer State 설정
  - Depth Stencil State 설정
  - Blend State 설정
  - Sampler State 설정
  - Input Layout 설정
  - Shader 설정 (VS, PS, GS, CS)
  - 각 상태의 역할과 설정 방법
  - 상태 변경의 성능 영향

### 2.6 DirectX 11 특화

#### ❌ DirectX 11 특화
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - Device Context의 역할
  - Immediate Context vs Deferred Context
  - Deferred Context의 사용 사례
  - Compute Shader 개념과 사용법
  - Geometry Shader 사용
  - Tessellation (Hull Shader, Domain Shader)
  - Multi-threading과 Deferred Context
  - DirectX 11의 성능 특성

### 2.7 DirectX 12 특화

#### ❌ DirectX 12 특화
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - Low-level API의 특징과 장단점
  - Command Queue 개념
  - Command List와 Command Allocator
  - Resource Barrier의 필요성
  - Descriptor Heap 개념과 종류
  - Root Signature 개념
  - Pipeline State Object (PSO)
  - Multi-threaded command recording
  - GPU와 CPU 동기화 최소화
  - DirectX 12의 성능 이점과 복잡도

### 2.8 DirectX 성능 최적화

#### ❌ DirectX 성능 최적화
- **현재 상태**: 완전히 누락
- **필수 주제**:
  - Draw Call 최적화 방법
  - Instancing을 통한 Draw Call 감소
  - 리소스 바인딩 최적화
  - GPU와 CPU 동기화 최소화
  - Flush와 Finish의 차이
  - GPU 타임라인 최적화
  - 메모리 대역폭 최적화
  - 텍스처 압축과 메모리 관리
  - DirectX 12의 성능 최적화 기법

### 2.9 누락 주제 요약

**우선순위 매우 높음:**
1. DirectX 기본 개념
2. DirectX 버전별 차이 (9/11/12)
3. DirectX API 기본 (Device, Context, 기본 리소스)
4. DirectX 리소스 관리 (Buffer, Texture)

**우선순위 높음:**
5. DirectX 렌더링 상태 설정
6. DirectX 11 특화 (Device Context, Compute Shader)
7. DirectX 성능 최적화

**우선순위 중간:**
8. DirectX 12 특화 (Low-level API, Command List, Descriptor Heap)

---

## 3. 재구성된 커리큘럼 구조 (restructure_curriculum)

### 3.1 재구성 원칙

1. **논리적 순서**: 기본 개념 → 버전 비교 → API 사용 → 리소스 관리 → 버전별 특화 → 성능 최적화
2. **개념 흐름**: DirectX 소개 → 버전 이해 → API 사용법 → 리소스 관리 → 고급 기능 → 최적화
3. **실무 적용**: 각 섹션 마지막에 실무 판단 질문 포함
4. **Windows 게임 개발 관점**: Windows 플랫폼 특화 내용 중심

### 3.2 재구성된 파일 구조

#### Part 1: DirectX 기본

1. `01.DirectX_기본개념.md` - DirectX란 무엇인가, 컴포넌트, OpenGL 비교 ❌ (신규)

**학습 목표:**
- DirectX의 개념과 역할 이해
- DirectX의 주요 컴포넌트 파악
- Windows 게임 개발에서 DirectX 선택 이유 이해
- DirectX vs OpenGL 비교

2. `02.DirectX_버전차이.md` - DirectX 9/11/12 비교 ❌ (신규)

**학습 목표:**
- 각 DirectX 버전의 주요 특징 이해
- 버전별 차이점과 변화 파악
- 언제 어떤 버전을 사용하는지 판단 능력
- 버전별 성능 특성 이해

#### Part 2: DirectX API 사용

3. `03.DirectX_API_기본.md` - Device, Context, 기본 리소스 생성 ❌ (신규)

**학습 목표:**
- Device와 Context 개념 이해
- 기본 리소스 생성 과정 이해
- Swap Chain, Render Target View 생성
- 기본 렌더링 루프 구조 이해

4. `04.DirectX_리소스관리.md` - Buffer, Texture 리소스 관리 ❌ (신규)

**학습 목표:**
- Vertex Buffer, Index Buffer 생성 및 사용
- Constant Buffer 개념과 사용법
- Texture 리소스 관리
- 리소스 바인딩 방법
- 리소스 생명주기 관리

#### Part 3: DirectX 버전별 특화

5. `05.DirectX11_특화.md` - DirectX 11의 특징과 사용법 ❌ (신규)

**학습 목표:**
- Device Context의 역할 이해
- Immediate Context vs Deferred Context
- Compute Shader 사용법
- DirectX 11의 고급 기능 이해

6. `06.DirectX12_특화.md` - DirectX 12의 Low-level API ❌ (신규)

**학습 목표:**
- Low-level API의 특징 이해
- Command Queue, Command List 개념
- Resource Barrier의 필요성
- Descriptor Heap 사용법
- Multi-threaded command recording

#### Part 4: 성능 최적화

7. `07.DirectX_성능최적화.md` - Draw Call, 동기화, 최적화 기법 ❌ (신규)

**학습 목표:**
- Draw Call 최적화 방법
- GPU와 CPU 동기화 최소화
- 리소스 바인딩 최적화
- 메모리 관리 최적화
- 실무 성능 최적화 기법

### 3.3 파일 구조 요약

**총 7개 파일:**
- `01.DirectX_기본개념.md`
- `02.DirectX_버전차이.md`
- `03.DirectX_API_기본.md`
- `04.DirectX_리소스관리.md`
- `05.DirectX11_특화.md`
- `06.DirectX12_특화.md`
- `07.DirectX_성능최적화.md`

**학습 순서:**
1. 기본 개념 → 2. 버전 비교 → 3. API 사용 → 4. 리소스 관리 → 5. 버전별 특화 → 6. 성능 최적화

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
- **심화 개념**: API 동작 원리, 내부 구조, 성능 특성 등
- **실무 적용**: 언제 사용하는지, 어떤 경우에 선택하는지

#### 질문 순서
1. 기본 개념 질문 (2-3개)
2. API 동작/사용법 질문 (3-5개)
3. 비교/차이점 질문 (2-4개)
4. 성능/최적화 질문 (2-3개)
5. 실무 적용/선택 기준 질문 (1-2개)
6. 에러 처리/예외 상황 질문 (해당되는 경우, 1-2개)
7. 요약 질문 (1개)

#### 필수 포함 질문 유형
- [ ] 기본 개념 질문 포함
- [ ] API 동작/사용법 질문 포함
- [ ] 비교/차이점 질문 포함 (해당되는 경우)
- [ ] 성능/최적화 질문 포함
- [ ] 실무 적용/선택 기준 질문 포함
- [ ] 에러 처리/예외 상황 질문 포함 (해당되는 경우)
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
- `## ✅ [API명] 동작` (또는 `## ✅ API 사용법`)
- `## ✅ [다른 방식]과의 비교` (해당되는 경우)
- `## ✅ 성능 / 최적화`
- `## ✅ 에러 처리 / 예외 상황` (해당되는 경우)
- `## ✅ 실무 / 설계 판단`
- `## ✅ 요약 질문`

**주제별 추가 카테고리:**
- DirectX API 관련: `## ✅ Device와 Context`, `## ✅ 리소스 생성`
- 버전 비교 관련: `## ✅ 버전별 특징`, `## ✅ 버전별 차이점`
- 성능 최적화 관련: `## ✅ Draw Call 최적화`, `## ✅ 동기화 최소화`

### 4.5 코드 예시 가이드라인

**코드 예시가 필요한 경우:**
- DirectX API 사용법 (Device 생성, 리소스 생성 등)
- 리소스 바인딩 패턴
- 렌더링 루프 구조
- 에러 처리 패턴

**코드 예시 형식:**
```cpp
// 간단한 설명
HRESULT hr = D3D11CreateDevice(
    nullptr,
    D3D_DRIVER_TYPE_HARDWARE,
    nullptr,
    0,
    nullptr,
    0,
    D3D11_SDK_VERSION,
    &device,
    nullptr,
    &context
);
if (FAILED(hr)) {
    // 에러 처리
}
```

---

## 5. 실행 계획

### Phase 1: 기획문서 작성 (우선순위: 높음)

1. **기획문서 작성 완료** ✅
   - 현재 상태 분석
   - 누락 주제 파악
   - 커리큘럼 구조 설계
   - 질문 형식 표준화

### Phase 2: 신규 파일 생성 (우선순위: 높음 → 중간)

**우선순위 매우 높음:**
1. `01.DirectX_기본개념.md` - DirectX 기본 개념
2. `02.DirectX_버전차이.md` - DirectX 버전별 차이

**우선순위 높음:**
3. `03.DirectX_API_기본.md` - DirectX API 기본
4. `04.DirectX_리소스관리.md` - DirectX 리소스 관리
5. `05.DirectX11_특화.md` - DirectX 11 특화

**우선순위 중간:**
6. `06.DirectX12_특화.md` - DirectX 12 특화
7. `07.DirectX_성능최적화.md` - DirectX 성능 최적화

### Phase 3: GPT 답변 작성 (우선순위: 높음)

1. **각 파일의 GPT 답변 섹션 완성**
   - 모든 질문에 대한 답변 작성
   - 카테고리별로 구분하여 작성
   - 간결하고 정확한 답변 제공

### Phase 4: 전체 검토 (우선순위: 중간)

1. **모든 파일의 질문 품질 검토**
   - 각 파일이 체크리스트를 만족하는지 확인
   - 질문의 깊이가 적절한지 확인

2. **중복 질문 제거**
   - 여러 파일에 걸쳐 중복된 질문 확인 및 정리
   - 그래픽스 폴더와의 중복 확인

3. **누락된 핵심 질문 추가**
   - 각 주제별로 면접에서 나올 수 있는 핵심 질문 확인
   - 던전앤파이터 등 실무 면접 질문 반영

4. **최종 정리**
   - 파일명 일관성 확인
   - 형식 일관성 확인
   - 내용 정확성 최종 검토

---

## 6. 체크리스트

각 파일마다 다음을 확인:

### 필수 체크리스트
- [ ] 기본 개념 질문 포함
- [ ] API 동작/사용법 질문 포함
- [ ] 비교/차이점 질문 포함 (해당되는 경우)
- [ ] 성능/최적화 질문 포함
- [ ] 실무 적용/선택 기준 질문 포함
- [ ] 에러 처리/예외 상황 질문 포함 (해당되는 경우)
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
- 예시: `01.DirectX_기본개념.md`, `05.DirectX11_특화.md`

### 마크다운 형식
- 제목: `# 🧠 [주제] 면접 질문 리스트`
- 카테고리: `## ✅ [카테고리명]`
- 질문: 번호와 함께 작성
- 사용자 답변: 4칸 들여쓰기
- GPT 답변: `<details>` 태그 내부에 작성

### 질문 작성 시 주의사항
- 면접에서 실제로 나올 수 있는 수준으로 작성
- 기본 개념부터 심화 개념까지 단계적으로 구성
- DirectX 질문은 실전 구현 경험을 중요시
- API 사용법과 에러 처리를 함께 다룸
- 성능과 최적화를 고려한 질문 포함
- Windows 게임 개발 관점에서 작성

### 플랫폼 고려사항
- Windows 플랫폼 중심으로 작성
- DirectX는 Windows 전용 API임을 명시
- 크로스 플랫폼 고려사항은 언급만 (OpenGL 비교 등)

### 그래픽스 폴더와의 관계
- 그래픽스 폴더: 렌더링 파이프라인, 셰이더 개념, 좌표계 변환 등 범용 그래픽스 이론
- DirectX 폴더: DirectX API 사용법, Device/Context, 리소스 관리, 버전별 차이 등 DirectX 특화 내용
- 두 폴더는 상호 보완적 관계로, 그래픽스 이론을 바탕으로 DirectX API를 학습

### 실무 면접 고려사항
- 던전앤파이터 등 Windows 게임 개발에서 DirectX는 필수
- DirectX에 대한 높은 이해도 요구
- 그래픽 퀄리티 향상 및 성능 최적화 경험 중요
- 실제 프로젝트에서의 DirectX 사용 경험 질문 예상
- 성능 병목 지점 찾기 및 최적화 경험 질문 예상

---

**문서 작성일**: 2026-01-09  
**최종 수정일**: 2026-01-09  
**버전**: 1.0
