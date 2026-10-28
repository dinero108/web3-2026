# 패스폴리오 v0.3

사이트: https://dinero108.github.io/web3-2026/

## 새 기능
이메일 회원가입·로그인·로그아웃, 비밀번호 재설정, Supabase 계정별 비공개 기록 저장을 구현했습니다. 게스트는 기존처럼 브라우저에 저장합니다. 로그인 후 게스트 기록은 자동 합치지 않으며, 포트폴리오 > 프로필 및 데이터 관리에서 가져올 수 있습니다.

**현재 인증 메일은 운영자 테스트 단계입니다.** Supabase 기본 SMTP는 조직 멤버 주소로만 보냅니다. 일반 가입과 비밀번호 재설정 서비스를 열기 전에 Authentication > Emails > SMTP Settings에서 발송 서비스를 연결하세요. 연결 후 auth-dialog.tsx의 테스트 단계 안내를 제거하고 다시 빌드합니다. 이메일 인증은 계속 활성화합니다.

## 실행과 배포
Node.js 24에서 `npm ci`, `npm test`, `npm run build`를 실행합니다. `npm run dev`는 로컬 개발 서버입니다.
GitHub Pages에 실행 파일을 올릴 경우 dist의 내용을 배포합니다. 원본 소스를 저장소에 올릴 경우 포함된 .github/workflows/pages.yml을 사용하고 Pages Source를 GitHub Actions로 변경합니다.

Supabase 프로젝트: uvzxyrbyszvmnlxchvoc (서울). 기본 공개 URL과 publishable key는 src/supabase.ts에 있습니다. VITE_SUPABASE_URL / VITE_SUPABASE_PUBLISHABLE_KEY로 재정의할 수 있습니다. 공개 키는 비밀번호가 아니며 각 사용자의 데이터 접근은 데이터베이스 RLS로 제한합니다. service_role, secret key, 메일 비밀번호는 클라이언트나 GitHub에 넣지 마세요.

Site URL과 허용 Redirect URL은 위 GitHub Pages 주소로 설정했습니다. 로컬에서 이메일 링크까지 테스트하려면 로컬 주소도 Supabase에 명시적으로 추가해야 합니다.

## 저장과 검증
supabase/001_portfolios.sql에 테이블과 소유자별 접근 정책이 있습니다. 현재 프로젝트에는 이미 적용했으므로 재실행하지 마세요. 기록 전체 삭제는 계정의 기록 내용을 비우며 회원 계정 자체는 삭제하지 않습니다.

21개 로드맵 테스트와 5개 인증 상태 테스트가 포함됩니다. 인증 테스트는 계정 전환, 늦게 도착한 조회·저장 응답, 로그아웃, 게스트 기록 분리, 조회 실패 시 덮어쓰기 방지를 검사합니다. 실제 데이터베이스에서 다른 계정의 조회·수정·삭제·삽입 차단과 비로그인 접근 차단을 검사했으며 테스트 데이터는 트랜잭션 롤백했습니다.

메일 가입·인증 링크·비밀번호 재설정의 실제 발송 검증은 발송 서비스 연결 후 필요합니다.
추천은 규칙형입니다. 생성형 AI, 기관 인증, SBT 발급은 아직 연결되지 않았습니다.


수정 가능한 소스는 pathfolio-source.zip에 들어 있습니다. 현재 저장소는 실행 파일 배포 방식(main / root)입니다.
