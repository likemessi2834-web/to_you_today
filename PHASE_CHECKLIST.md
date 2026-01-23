# Phase 체크리스트

이 문서는 각 개발 단계(Phase)의 완료 상태를 추적합니다.

## Phase 0: 프로젝트 구조 및 가드레일 설정

**시작일**: [Phase 0 시작 시점]  
**목표 완료일**: [목표 날짜]

### DoD 체크리스트

#### 공통 DoD
- [ ] `flutter pub get` 성공
- [ ] `flutter analyze` 에러 없이 통과
- [ ] `flutter run -d chrome` 정상 실행 (크래시 없음)
- [ ] `flutter build apk --debug` 성공 (가능한 경우)

#### Phase 0 특화 DoD
- [ ] `docs/README.md` 생성 및 내용 확인
- [ ] `docs/PHASES.md` 생성 및 내용 확인
- [ ] `docs/DOD.md` 생성 및 내용 확인
- [ ] `FEATURES.md` 생성 및 내용 확인
- [ ] `PHASE_CHECKLIST.md` 생성 및 내용 확인 (이 파일)
- [ ] `CONTRIBUTING.md` 또는 `DEV_GUIDE.md` 생성 및 내용 확인
- [ ] 사용하지 않는 import 제거
- [ ] 명백한 린트 경고 해결
- [ ] 기존 기능 동작 변경 없음 확인

### 완료 상태
- [ ] **Phase 0 완료** (모든 체크리스트 통과)

**완료일**: [완료 시 날짜 기록]  
**검증자**: [검증한 사람]

---

## Phase 1: (향후 정의)

**시작일**: TBD  
**목표 완료일**: TBD

### DoD 체크리스트

#### 공통 DoD
- [ ] `flutter pub get` 성공
- [ ] `flutter analyze` 에러 없이 통과
- [ ] `flutter run -d chrome` 정상 실행 (크래시 없음)
- [ ] `flutter build apk --debug` 성공 (가능한 경우)

#### Phase 1 특화 DoD
- [ ] TBD - Phase 1 시작 시 추가

### 완료 상태
- [ ] **Phase 1 완료** (모든 체크리스트 통과)

**완료일**: TBD  
**검증자**: TBD

---

## Phase 2: (향후 정의)

**시작일**: TBD  
**목표 완료일**: TBD

### DoD 체크리스트

#### 공통 DoD
- [ ] `flutter pub get` 성공
- [ ] `flutter analyze` 에러 없이 통과
- [ ] `flutter run -d chrome` 정상 실행 (크래시 없음)
- [ ] `flutter build apk --debug` 성공 (가능한 경우)

#### Phase 2 특화 DoD
- [ ] TBD - Phase 2 시작 시 추가

### 완료 상태
- [ ] **Phase 2 완료** (모든 체크리스트 통과)

**완료일**: TBD  
**검증자**: TBD

---

## 사용 방법

1. 각 Phase 시작 시 해당 섹션의 체크리스트를 사용
2. 작업 완료 시 체크박스에 체크 표시
3. 모든 체크리스트 완료 후 "완료 상태" 섹션에 체크
4. 완료일과 검증자 기록

## 주의사항

- **모든 체크리스트를 통과해야만** Phase가 완료된 것으로 간주됩니다
- DoD 실패 시 해당 항목을 수정한 후 재검증해야 합니다
- 다음 Phase로 진행하기 전에 사용자 승인이 필요합니다
