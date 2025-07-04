# 작심큰일 챌린지 - 문제 풀이 공간

> Django 기반 경량 웹 서비스로 구현된 코딩 문제 풀이 플랫폼

## 📋 프로젝트 개요

SCC의 온라인 강의 → 내배캠 파이프라인으로 유입하기 위한 저비용 고효율 프로그램입니다. 참가자들이 매일 코딩 문제를 풀고 성취감을 얻을 수 있도록 설계된 가볍고 직관적인 웹 서비스입니다.

## 🎯 주요 기능

### 👥 참가자 기능
- **문제 조회**: 매일 오전 9시 언어/레벨별 문제 공개
- **풀이 제출**: 코드 링크 제출 + 난이도 피드백
- **TIL 작성**: 주 1회 블로그 링크 제출 (회고)
- **시니어 해설**: 제출 완료 후 전문가 풀이 열람
- **커뮤니티**: 다른 참가자들의 코드 확인 및 좋아요
- **마이페이지**: 개인 진행 현황 및 리워드 확인

### 🛠️ 운영진 기능
- **문제 관리**: 문제 등록/수정/공개
- **진행 현황**: 참가자 인증 현황 관리
- **통계 분석**: 제출률, 완주율 등 데이터 확인
- **외부 연동**: Slack/CRM/Discord 알림 발송

## 🏗️ 시스템 아키텍처

```
[사용자 브라우저]
    ↓ HTML (Django Template)
[Django App (Gunicorn)]
    ↓ ORM
[PostgreSQL DB (Railway)]
    ↘ Slack Webhook / Discord CRM
```

## 🛠️ 기술 스택

| 계층 | 기술 | 비고 |
|------|------|------|
| **Frontend** | Django Template + Tailwind CSS | 모바일 반응형 대응 |
| **Backend** | Django 4.x | MTV 패턴 기반 |
| **Database** | PostgreSQL (Railway) | ORM 기반 모델 설계 |
| **Authentication** | Django Auth + 연락처 기반 식별 | Discord OAuth 추후 도입 고려 |
| **DevOps** | Railway (GitHub Actions + Gunicorn + Whitenoise) | 자동 배포, 정적 파일 처리 |
| **Integration** | Slack Webhook / Discord | 알림 및 커뮤니티 운영 |

## 📊 데이터베이스 설계

### 주요 모델
- **User**: 참가자 정보 (이름/연락처/이메일/닉네임/레벨)
- **Problem**: 매일 출제 문제 (언어/레벨/출처/설명/출제일)
- **Submission**: 제출 풀이 (링크 + 난이도 평가 + 제출 시간)
- **TIL**: 주차별 TIL 제출 (인증 여부 포함)
- **SeniorSolution**: 시니어 해설 (권한 제한 열람)
- **AuthLog**: 로그인 기록 및 접속 시점
- **GiftRecord**: 리워드 수령 내역

## 🎨 주요 페이지

### 📱 사용자 인터페이스
1. **로그인 페이지**: 이메일/연락처 기반 인증
2. **오늘의 문제**: 언어/레벨별 일일 문제 + 진행 현황
3. **문제 풀이 공간**: 실시간 타이머 + IDE 환경
4. **내 제출 기록**: 개인 풀이 히스토리 + 통계
5. **TIL 제출**: 블로그 링크 제출 + 현황 관리
6. **마이페이지**: 진행률 + 리워드 현황

### 🔧 특별 기능
- **타이머 시스템**: 문제 풀이 시간 정확 측정
- **코드 하이라이팅**: Python 문법 하이라이팅 지원
- **자동 저장**: 30초마다 코드 임시 저장
- **커뮤니티**: 다른 참가자 코드 열람 + 좋아요
- **시니어 해설**: 전문가 풀이 + 성능 분석

## 🚀 설치 및 실행

### 요구사항
- Python 3.8+
- Django 4.x
- PostgreSQL
- Node.js (Tailwind CSS)

### 로컬 개발 환경 설정
```bash
# 저장소 클론
git clone [repository-url]
cd 작심큰일-문제풀이공간

# 가상환경 생성 및 활성화
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 의존성 설치
pip install -r requirements.txt

# 데이터베이스 마이그레이션
python manage.py migrate

# 개발 서버 실행
python manage.py runserver
```

### 환경 변수 설정
```bash
# .env 파일 생성
DATABASE_URL=postgresql://...
SECRET_KEY=your-secret-key
SLACK_WEBHOOK_URL=https://hooks.slack.com/...
DISCORD_WEBHOOK_URL=https://discord.com/api/webhooks/...
```

## 📈 운영 및 모니터링

### 운영 주체
- **교육운영실**: 콘텐츠/참여 관리
- **개발지원팀**: 시스템 유지보수

### 알림 시스템
- **Slack 연동**: 인증 완료자 → 특정 채널 메시지
- **CRM 연동**: 이메일/연락처 기반 유저 매핑
- **Discord**: 참가자 커뮤니티 운영

### 모니터링
- Django 기본 로그 + Railway 로그 콘솔
- 실시간 참여율 및 완주율 추적
- 에러 로깅 및 성능 모니터링

## 🎁 리워드 시스템

### 달성 조건
- **문제 풀이 완주**: 내일배움캠프 할인쿠폰
- **TIL 완주**: 스타벅스 아메리카노
- **연속 제출**: 메가커피 쿠폰
- **커뮤니티 활동**: 추가 리워드

## 📞 문의 및 지원

- **교육운영실**: 콘텐츠 관련 문의
- **개발지원팀**: 시스템 오류 신고
- **Discord**: 참가자 간 소통 채널

---

## 📄 라이선스

이 프로젝트는 교육 목적으로 제작되었습니다.

**© 2025 스파르타코딩클럽 - 작심큰일 챌린지**
