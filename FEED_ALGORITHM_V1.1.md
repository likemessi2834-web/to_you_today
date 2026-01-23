# Feed Algorithm V1.1 구현 가이드

## 개요
"오늘의 당신에게" 앱의 홈 피드 알고리즘 V1.1이 구현되었습니다. 이 알고리즘은 3가지 풀(P1, P2, P3)에서 데이터를 가져와 개인화된 피드를 생성합니다.

## 구현된 파일

### 1. 모델 업데이트
- **`lib/models/post_model.dart`**: 
  - `viewCount`, `isPublic`, `allowSave`, `allowShare`, `categoryId`, `saveCount` 필드 추가
  - Firestore 호환성을 위한 getter 및 toFirestore 메서드 업데이트

- **`lib/models/user_model.dart`**: 
  - `preferredCategoriesScore` 필드 추가
  - `preferredCategories` getter 추가 (상위 3개 카테고리 반환)

### 2. Repository 패턴
- **`lib/services/feed_repository.dart`**: 
  - P1 (Personalization, 70%): 사용자 선호 카테고리 기반 쿼리
  - P2 (Freshness, 20%): 최신순 정렬
  - P3 (Quality, 10%): 저장 많은 순 (allowSave=true만)
  - Pagination 지원
  - Safety Filter를 위한 blockedUsers, hiddenPosts 조회

### 3. Service 레이어
- **`lib/services/feed_service.dart`**: 
  - Ranking (Scoring): 점수 계산 및 Tie-breaker 처리
  - Blending & Filtering: Safety Filter, Fatigue Policy 적용
  - Fatigue Policy: 동일 카테고리 3개 연속 시 다른 카테고리 삽입

### 4. Firestore 인덱스
- **`firestore.indexes.json`**: 필요한 복합 인덱스 정의
- **`firebase.json`**: 인덱스 파일 경로 추가

## 사용 방법

```dart
import 'package:to_you_today/services/feed_service.dart';
import 'package:firebase_auth/firebase_auth.dart';

final feedService = FeedService();
final userId = FirebaseAuth.instance.currentUser?.uid;

if (userId != null) {
  final feedPosts = await feedService.generateFeed(
    userId: userId,
    targetSize: 50,
  );
  // feedPosts를 UI에 표시
}
```

## Firestore 데이터 구조

### `posts` Collection
다음 필드들이 반드시 필요합니다:
- `isPublic` (boolean): 홈 화면 공개 여부
- `allowSave` (boolean): 저장 허용 여부
- `allowShare` (boolean): 공유 허용 여부
- `categoryId` (string): 카테고리 식별자 (또는 `category` 필드 사용 가능)
- `viewCount` (number): 조회 수 (Tie-breaker에 사용)
- `saveCount` (number): 저장 수
- `createdAt` (timestamp): 생성일

### `users` Collection
- `preferred_categories_score` (map<string, double>): 카테고리별 선호도 점수
  - 예: `{"안부": 0.8, "인사": 0.6, "격려": 0.4}`

## 필수 Firestore 인덱스

다음 인덱스들이 필요합니다 (자동 생성됨):

1. **P1 쿼리용**:
   - Collection: `posts`
   - Fields: `isPublic` (Asc), `categoryId` (Asc), `createdAt` (Desc)

2. **P2 쿼리용**:
   - Collection: `posts`
   - Fields: `isPublic` (Asc), `createdAt` (Desc)

3. **P3 쿼리용**:
   - Collection: `posts`
   - Fields: `isPublic` (Asc), `allowSave` (Asc), `saveCount` (Desc)

인덱스가 없으면 에러 메시지에 생성 링크가 포함됩니다.

## 알고리즘 상세

### 1. Candidate Generation (70:20:10 비율)
- **P1 (70%)**: 사용자의 `preferredCategories`에 해당하는 게시물
- **P2 (20%)**: 최신순 정렬
- **P3 (10%)**: 저장 많은 순 (단, `allowSave=true`만)

### 2. Ranking (Scoring)
- **기본 점수**: `longTermCatScore` (70%) + `recencyBoost` (30%)
- **Tie-breaker**: 점수가 같을 경우 `viewCount`가 높은 순서

### 3. Blending & Filtering
- **Safety Filter**: 
  - `blockedUsers` (차단한 유저) 제외
  - `hiddenPosts` (숨긴 게시물) 제외
  - `isPublic=false` 제외
- **Fatigue Policy**: 
  - 동일 카테고리 게시물이 연속으로 3개 배치되면, 
  - 그 다음(4번째) 게시물은 반드시 다른 카테고리의 게시물을 삽입

## 주의사항

1. **인덱스 생성**: Firestore 콘솔에서 인덱스가 자동 생성될 때까지 몇 분이 걸릴 수 있습니다.
2. **데이터 마이그레이션**: 기존 게시물에 `categoryId`, `isPublic`, `allowSave`, `allowShare` 필드를 추가해야 합니다.
3. **사용자 온보딩**: 가입 시 `preferred_categories_score`를 초기값으로 설정해야 합니다.
4. **viewCount 업데이트**: 상세 진입 시 `FieldValue.increment(1)`을 사용하여 업데이트하세요.

## 다음 단계

1. 기존 `FirebaseService.getPostsStream()`을 `FeedService.generateFeed()`로 교체
2. Firestore 인덱스 배포: `firebase deploy --only firestore:indexes`
3. 데이터 마이그레이션 스크립트 실행 (필요 시)
4. 사용자 온보딩 플로우에 `preferredCategoriesScore` 설정 추가
