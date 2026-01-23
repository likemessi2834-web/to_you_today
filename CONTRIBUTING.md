# 기여 가이드 (Contributing Guide)

이 문서는 프로젝트에 기여하기 위한 가이드라인을 제공합니다.

## 커밋 메시지 컨벤션

모든 커밋 메시지는 다음 형식을 따릅니다:

```
phase-x: <short message>
```

### 형식 설명

- **phase-x**: 현재 작업 중인 Phase 번호 (예: `phase-0`, `phase-1`)
- **<short message>**: 변경사항을 간결하게 설명하는 메시지

### 예시

```
phase-0: Add project documentation structure
phase-0: Fix lint warnings in main.dart
phase-1: Add user authentication flow
phase-1: Implement photo upload feature
```

### 커밋 메시지 작성 원칙

1. **명확성**: 무엇을 변경했는지 명확히 표현
2. **간결성**: 한 줄로 요약 가능하도록 작성
3. **일관성**: 항상 `phase-x:` 접두사 사용
4. **영어 사용**: 커밋 메시지는 영어로 작성 (선택사항이지만 권장)

## 개발 워크플로우

### 1. 작업 시작 전

- `docs/PHASES.md`에서 현재 Phase의 범위 확인
- `FEATURES.md`에서 기능 명세 확인
- `PHASE_CHECKLIST.md`에서 진행 상황 확인

### 2. 코드 작성

- 기존 코드 스타일 준수
- `flutter analyze`로 정적 분석 확인
- 명확한 변수명과 함수명 사용
- 주석은 필요한 경우에만 추가 (자명한 코드는 주석 불필요)

### 3. 커밋 전 확인

- [ ] `flutter pub get` 실행
- [ ] `flutter analyze` 에러 없이 통과
- [ ] 변경사항이 의도한 대로 동작하는지 확인
- [ ] 커밋 메시지가 컨벤션을 따르는지 확인

### 4. Phase 완료 시

- [ ] `docs/DOD.md`의 해당 Phase 체크리스트 모두 통과
- [ ] `PHASE_CHECKLIST.md`에서 완료 상태 업데이트
- [ ] 관련 문서 업데이트 (필요한 경우)

## 코드 스타일

### Dart/Flutter 컨벤션

- Dart 공식 스타일 가이드 준수
- `analysis_options.yaml`의 린트 규칙 준수
- 들여쓰기: 2 spaces

### 파일 구조

- 각 주요 기능은 별도 파일로 분리
- 파일명: `snake_case.dart`
- 클래스명: `PascalCase`

### 상태 관리

- 현재는 StatefulWidget 기반
- 향후 필요 시 Riverpod 도입 검토 (Phase 0에서는 추가하지 않음)

## Pull Request (향후 사용 시)

PR 제목도 커밋 메시지 컨벤션을 따릅니다:

```
phase-x: <short description>
```

PR 본문에는:
- 변경사항 요약
- 테스트 방법
- 관련 이슈 번호 (있는 경우)

## 질문 및 지원

프로젝트 관련 질문이 있으면:
1. `docs/README.md` 확인
2. `docs/PHASES.md`에서 현재 Phase 확인
3. 필요 시 이슈 생성 또는 팀에 문의

## Phase별 제약사항

각 Phase는 명확한 범위와 제약사항이 있습니다. `docs/PHASES.md`를 참고하여 현재 Phase의 제약사항을 준수하세요.

### Phase 0 제약사항 예시

- ❌ Firebase 추가 금지
- ❌ UGC 기능 추가 금지
- ❌ 포인트 시스템 추가 금지
- ❌ AdMob 통합 금지
- ❌ 주요 UI 리팩토링 금지

## 감사합니다!

프로젝트에 기여해 주셔서 감사합니다. 모든 기여는 프로젝트의 성장에 도움이 됩니다.
