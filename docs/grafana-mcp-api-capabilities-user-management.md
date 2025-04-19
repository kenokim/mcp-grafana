# Grafana MCP API 기능 목록: 사용자 및 팀 관리

이 문서는 MCP(Model Context Protocol)를 통해 Grafana에서 제공할 수 있는 사용자 및 팀 관리 관련 기능들을 상세히 정리한 것입니다.

## 사용자 및 팀 관리

### 사용자 관리

401. **사용자 목록 조회** (`list_users`)
    - 모든 Grafana 사용자 조회
    - 매개변수: `query`, `limit`, `page`
    - 예시: 모든 활성 사용자 목록 조회

402. **사용자 상세 조회** (`get_user`)
    - 특정 사용자의 상세 정보 조회
    - 매개변수: `user_id`
    - 예시: 사용자의 역할, 권한, 조직 정보 조회

403. **사용자 생성** (`create_user`)
    - 새 Grafana 사용자 생성
    - 매개변수: `name`, `email`, `login`, `password`
    - 예시: 새 팀원을 위한 사용자 계정 생성

404. **사용자 업데이트** (`update_user`)
    - 기존 사용자 정보 수정
    - 매개변수: `user_id`, `name`, `email`, `login`
    - 예시: 사용자 이름 또는 이메일 업데이트

405. **사용자 삭제** (`delete_user`)
    - 사용자 계정 삭제
    - 매개변수: `user_id`
    - 예시: 퇴사한 직원의 계정 제거

406. **사용자 비밀번호 변경** (`change_user_password`)
    - 사용자 비밀번호 변경
    - 매개변수: `user_id`, `new_password`
    - 예시: 보안 정책에 따른 비밀번호 재설정

407. **사용자 조직 관리** (`manage_user_organizations`)
    - 사용자의 조직 멤버십 관리
    - 매개변수: `user_id`, `organizations_to_add`, `organizations_to_remove`
    - 예시: 사용자를 새 조직에 추가

408. **사용자 권한 조회** (`get_user_permissions`)
    - 사용자의 권한 목록 조회
    - 매개변수: `user_id`
    - 예시: 특정 사용자가 접근할 수 있는 대시보드 및 기능 확인

409. **사용자 활동 로그 조회** (`get_user_activity`)
    - 사용자 활동 이력 조회
    - 매개변수: `user_id`, `time_range`, `limit`
    - 예시: 사용자의 로그인 이력 및 대시보드 접근 이력 조회

410. **사용자 인증 토큰 관리** (`manage_user_auth_tokens`)
    - 사용자의 API 키 및 인증 토큰 관리
    - 매개변수: `user_id`, `token_name`, `role`, `expiration`
    - 예시: 사용자를 위한 새 API 키 생성

411. **사용자 프로필 업데이트** (`update_user_profile`)
    - 사용자 프로필 정보 수정
    - 매개변수: `user_id`, `theme`, `timezone`, `language`
    - 예시: 사용자 인터페이스 언어 변경

412. **사용자 환경 설정 관리** (`manage_user_preferences`)
    - 사용자 대시보드 및 알림 환경 설정 관리
    - 매개변수: `user_id`, `preferences`
    - 예시: 기본 시간 범위 및 새로 고침 간격 설정

413. **사용자 로그인 이력 조회** (`get_user_login_history`)
    - 사용자 로그인 시도 이력 조회
    - 매개변수: `user_id`, `time_range`, `limit`
    - 예시: 실패한 로그인 시도 확인

414. **사용자 대시보드 권한 관리** (`manage_user_dashboard_permissions`)
    - 사용자에게 특정 대시보드에 대한 권한 부여/제거
    - 매개변수: `user_id`, `dashboard_uid`, `permission_level`
    - 예시: 사용자에게 특정 대시보드 편집 권한 부여

415. **사용자 데이터 소스 권한 관리** (`manage_user_datasource_permissions`)
    - 사용자의 데이터 소스 접근 권한 관리
    - 매개변수: `user_id`, `datasource_uid`, `permission_level`
    - 예시: 사용자에게 중요 데이터 소스 읽기 권한 부여

416. **사용자 알림 설정 관리** (`manage_user_notification_settings`)
    - 사용자 알림 수신 설정 관리
    - 매개변수: `user_id`, `notification_channels`, `email_settings`
    - 예시: 사용자의 이메일 알림 설정 구성

417. **사용자 온보딩 상태 관리** (`manage_user_onboarding_state`)
    - 사용자 온보딩 프로세스 상태 관리
    - 매개변수: `user_id`, `onboarding_state`
    - 예시: 새 사용자를 위한 튜토리얼 완료 상태 업데이트

418. **사용자 세션 관리** (`manage_user_sessions`)
    - 사용자 활성 세션 관리
    - 매개변수: `user_id`, `action`
    - 예시: 사용자의 모든 활성 세션 종료

419. **사용자 할당량 설정** (`set_user_quota`)
    - 개별 사용자의 리소스 사용 할당량 설정
    - 매개변수: `user_id`, `quota_target`, `limit`
    - 예시: 사용자당 생성 가능한 대시보드 수 제한

420. **서비스 계정 관리** (`manage_service_accounts`)
    - 서비스 계정 관리
    - 매개변수: `action`, `account_id`, `name`, `role`
    - 예시: 자동화 작업을 위한 서비스 계정 생성

### 팀 관리

421. **팀 목록 조회** (`list_teams`)
    - 모든 Grafana 팀 조회
    - 매개변수: `query`, `limit`, `page`
    - 예시: 모든 팀 목록 및 멤버 수 조회

422. **팀 상세 조회** (`get_team`)
    - 특정 팀의 상세 정보 조회
    - 매개변수: `team_id`
    - 예시: 팀 멤버, 권한, 관련 폴더 정보 조회

423. **팀 생성** (`create_team`)
    - 새 Grafana 팀 생성
    - 매개변수: `name`, `email`, `org_id`
    - 예시: 새 부서를 위한 모니터링 팀 생성

424. **팀 업데이트** (`update_team`)
    - 기존 팀 정보 수정
    - 매개변수: `team_id`, `name`, `email`
    - 예시: 팀 이름 변경

425. **팀 삭제** (`delete_team`)
    - 팀 삭제
    - 매개변수: `team_id`
    - 예시: 더 이상 필요 없는 팀 제거

426. **팀 멤버 조회** (`get_team_members`)
    - 팀 멤버 목록 조회
    - 매개변수: `team_id`
    - 예시: 팀에 속한 모든 사용자 조회

427. **팀 멤버 추가** (`add_team_member`)
    - 팀에 멤버 추가
    - 매개변수: `team_id`, `user_id`
    - 예시: 새 팀원 추가

428. **팀 멤버 제거** (`remove_team_member`)
    - 팀에서 멤버 제거
    - 매개변수: `team_id`, `user_id`
    - 예시: 팀에서 사용자 제거

429. **팀 권한 설정** (`set_team_permissions`)
    - 팀에 대한 권한 구성
    - 매개변수: `team_id`, `permission`
    - 예시: 팀에 대시보드 편집 권한 부여

430. **팀 할당량 설정** (`set_team_quota`)
    - 팀의 리소스 사용 할당량 설정
    - 매개변수: `team_id`, `quota_target`, `limit`
    - 예시: 팀당 대시보드 최대 수 설정

431. **팀 동기화 설정** (`configure_team_sync`)
    - 외부 인증 시스템과 팀 동기화 구성
    - 매개변수: `team_id`, `sync_provider`, `sync_groups`
    - 예시: LDAP 그룹과 Grafana 팀 동기화 설정

432. **팀 대시보드 접근 관리** (`manage_team_dashboard_access`)
    - 팀의 대시보드 접근 권한 관리
    - 매개변수: `team_id`, `dashboard_uid`, `permission_level`
    - 예시: 팀에 특정 대시보드 편집 권한 부여

433. **팀 폴더 접근 관리** (`manage_team_folder_access`)
    - 팀의 폴더 접근 권한 관리
    - 매개변수: `team_id`, `folder_uid`, `permission_level`
    - 예시: 팀에 특정 폴더의 대시보드 생성 권한 부여

434. **팀 알림 수신 설정** (`configure_team_notifications`)
    - 팀 알림 수신 설정 관리
    - 매개변수: `team_id`, `notification_channels`
    - 예시: 팀 이메일 및 Slack 채널 구성

435. **팀 활동 로그 조회** (`get_team_activity`)
    - 팀 멤버의 활동 이력 조회
    - 매개변수: `team_id`, `time_range`, `limit`
    - 예시: 팀 멤버가 수행한 대시보드 편집 이력 조회

436. **팀 대시보드 공유** (`share_dashboard_with_team`)
    - 대시보드를 특정 팀과 공유
    - 매개변수: `dashboard_uid`, `team_id`, `permission_level`
    - 예시: 중요 모니터링 대시보드를 운영팀과 공유

437. **팀 내보내기** (`export_team`)
    - 팀 구성 및 권한 내보내기
    - 매개변수: `team_id`, `include_members`
    - 예시: 팀 구성을 다른 Grafana 인스턴스로 이전하기 위한 내보내기

438. **팀 가져오기** (`import_team`)
    - 팀 구성 가져오기
    - 매개변수: `team_json`, `update_existing`
    - 예시: 내보낸 팀 구성 가져오기

439. **팀 역할 할당** (`assign_team_role`)
    - 팀에 역할 할당
    - 매개변수: `team_id`, `role_id`, `scope`
    - 예시: 팀에 편집자 역할 부여

440. **팀 프로젝트 할당** (`assign_team_to_project`)
    - 팀을 특정 프로젝트에 할당
    - 매개변수: `team_id`, `project_id`, `role`
    - 예시: 개발팀을 애플리케이션 모니터링 프로젝트에 할당

### 역할 및 권한 관리

441. **역할 목록 조회** (`list_roles`)
    - 모든 Grafana 역할 조회
    - 매개변수: `none`
    - 예시: 시스템에 구성된 모든 역할 목록 조회

442. **역할 상세 조회** (`get_role`)
    - 특정 역할의 상세 정보 조회
    - 매개변수: `role_id`
    - 예시: 역할의 권한 및 제한 사항 조회

443. **역할 생성** (`create_role`)
    - 새 역할 생성
    - 매개변수: `name`, `description`, `permissions`, `hidden`
    - 예시: 읽기 전용 역할 생성

444. **역할 업데이트** (`update_role`)
    - 기존 역할 수정
    - 매개변수: `role_id`, `name`, `description`, `permissions`
    - 예시: 역할에 새 권한 추가

445. **역할 삭제** (`delete_role`)
    - 역할 삭제
    - 매개변수: `role_id`
    - 예시: 사용하지 않는 역할 제거

446. **역할 할당** (`assign_role`)
    - 사용자에게 역할 할당
    - 매개변수: `user_id`, `role_id`, `scope`
    - 예시: 사용자에게 관리자 역할 부여

447. **역할 할당 취소** (`revoke_role`)
    - 사용자에게서 역할 회수
    - 매개변수: `user_id`, `role_id`, `scope`
    - 예시: 사용자의 관리자 권한 제거

448. **역할 할당 조회** (`list_role_assignments`)
    - 역할 할당 목록 조회
    - 매개변수: `user_id`, `role_id`, `scope`
    - 예시: 특정 역할이 할당된 모든 사용자 조회

449. **권한 목록 조회** (`list_permissions`)
    - 시스템의 모든 권한 목록 조회
    - 매개변수: `none`
    - 예시: 모든 가능한 권한 및 설명 조회

450. **권한 체크** (`check_permission`)
    - 특정 사용자의 권한 확인
    - 매개변수: `user_id`, `action`, `scope`
    - 예시: 사용자가 대시보드를 편집할 수 있는지 확인

451. **권한 스코프 관리** (`manage_permission_scopes`)
    - 권한 스코프 설정 관리
    - 매개변수: `permission_id`, `scopes`
    - 예시: 특정 폴더나 대시보드로 권한 범위 제한

452. **기본 역할 설정** (`set_default_role`)
    - 새 사용자에게 자동 할당될 기본 역할 설정
    - 매개변수: `role_id`, `org_id`
    - 예시: 모든 새 사용자에게 뷰어 역할 부여

453. **역할 복제** (`clone_role`)
    - 기존 역할을 복제하여 새 역할 생성
    - 매개변수: `role_id`, `new_name`
    - 예시: 기존 편집자 역할을 기반으로 한 커스텀 역할 생성

454. **역할 권한 업데이트** (`update_role_permissions`)
    - 역할의 권한 세트 업데이트
    - 매개변수: `role_id`, `permissions_to_add`, `permissions_to_remove`
    - 예시: 역할에 데이터 소스 관리 권한 추가

455. **역할 기반 메뉴 접근 설정** (`configure_role_menu_access`)
    - 역할별 UI 메뉴 접근 설정
    - 매개변수: `role_id`, `menu_items`
    - 예시: 특정 역할에서 관리 메뉴 숨기기

456. **역할 그룹 관리** (`manage_role_groups`)
    - 역할 그룹 관리
    - 매개변수: `group_name`, `roles`
    - 예시: 관련 역할을 그룹화하여 관리

457. **RBAC 활성화/비활성화** (`toggle_rbac`)
    - 역할 기반 접근 제어 활성화 또는 비활성화
    - 매개변수: `enabled`
    - 예시: 세분화된 권한 제어를 위한 RBAC 활성화

458. **역할 권한 보고서 생성** (`generate_role_permissions_report`)
    - 역할 권한 할당 보고서 생성
    - 매개변수: `roles`, `format`
    - 예시: 감사를 위한 역할 및 권한 보고서 생성

459. **API 키 역할 할당** (`assign_role_to_api_key`)
    - API 키에 역할 할당
    - 매개변수: `api_key_id`, `role_id`
    - 예시: 자동화 스크립트 API 키에 제한된 권한 부여

460. **대시보드 권한 상속 설정** (`configure_dashboard_permission_inheritance`)
    - 대시보드 권한 상속 규칙 설정
    - 매개변수: `folder_uid`, `inheritance_mode`
    - 예시: 폴더 권한이 포함된 모든 대시보드에 상속되도록 설정

### 인증 및 인가 관리

461. **인증 설정 관리** (`manage_auth_settings`)
    - Grafana 인증 설정 관리
    - 매개변수: `auth_type`, `settings`
    - 예시: LDAP 인증 구성 업데이트

462. **OAuth 제공자 구성** (`configure_oauth_provider`)
    - OAuth 인증 제공자 구성
    - 매개변수: `provider_name`, `client_id`, `client_secret`, `auth_url`, `token_url`
    - 예시: GitHub OAuth 통합 설정

463. **LDAP 구성 관리** (`manage_ldap_config`)
    - LDAP 통합 설정 관리
    - 매개변수: `ldap_config`
    - 예시: 회사 LDAP 서버와 동기화 설정

464. **SAML 구성 관리** (`manage_saml_config`)
    - SAML 인증 구성 관리
    - 매개변수: `saml_config`
    - 예시: 기업 SAML IdP와 통합 설정

465. **SSO 설정 구성** (`configure_sso_settings`)
    - 단일 로그인 설정 구성
    - 매개변수: `provider`, `settings`
    - 예시: 회사 SSO 시스템과 통합

466. **다중 인증(MFA) 설정** (`configure_mfa`)
    - 다중 인증 설정 관리
    - 매개변수: `enabled`, `methods`
    - 예시: 관리자 계정에 대한 TOTP 인증 활성화

467. **인증 프록시 설정** (`configure_auth_proxy`)
    - 인증 프록시 설정 관리
    - 매개변수: `enabled`, `header_name`, `header_property`
    - 예시: 리버스 프록시를 통한 인증 설정

468. **API 키 관리** (`manage_api_keys`)
    - API 키 관리
    - 매개변수: `action`, `key_id`, `name`, `role`, `expiration`
    - 예시: 자동화용 API 키 생성

469. **서비스 계정 키 관리** (`manage_service_account_tokens`)
    - 서비스 계정 토큰 관리
    - 매개변수: `service_account_id`, `name`, `expiration`
    - 예시: CI/CD 파이프라인을 위한 서비스 계정 토큰 생성

470. **로그인 시도 모니터링** (`monitor_login_attempts`)
    - 로그인 시도 모니터링
    - 매개변수: `time_range`, `status`
    - 예시: 실패한 로그인 시도 모니터링

### 조직 관리

471. **조직 목록 조회** (`list_organizations`)
    - 모든 Grafana 조직 조회
    - 매개변수: `query`, `limit`, `page`
    - 예시: 모든 조직 및 사용자 수 조회

472. **조직 생성** (`create_organization`)
    - 새 Grafana 조직 생성
    - 매개변수: `name`
    - 예시: 새 사업부를 위한 조직 생성

473. **조직 상세 조회** (`get_organization`)
    - 특정 조직의 상세 정보 조회
    - 매개변수: `org_id`
    - 예시: 조직 사용자, 팀, 할당량 정보 조회

474. **조직 업데이트** (`update_organization`)
    - 기존 조직 정보 수정
    - 매개변수: `org_id`, `name`
    - 예시: 조직 이름 변경

475. **조직 삭제** (`delete_organization`)
    - 조직 삭제
    - 매개변수: `org_id`
    - 예시: 더 이상 필요 없는 조직 제거

476. **조직 사용자 목록 조회** (`list_organization_users`)
    - 조직 사용자 목록 조회
    - 매개변수: `org_id`
    - 예시: 조직의 모든 멤버 및 역할 조회

477. **조직에 사용자 추가** (`add_user_to_organization`)
    - 조직에 사용자 추가
    - 매개변수: `org_id`, `user_id`, `role`
    - 예시: 사용자를 조직에 편집자 역할로 추가

478. **조직 사용자 역할 업데이트** (`update_organization_user_role`)
    - 조직 내 사용자 역할 변경
    - 매개변수: `org_id`, `user_id`, `new_role`
    - 예시: 사용자 역할을 뷰어에서 편집자로 승격

479. **조직에서 사용자 제거** (`remove_user_from_organization`)
    - 조직에서 사용자 제거
    - 매개변수: `org_id`, `user_id`
    - 예시: 퇴사한 직원을 조직에서 제거

480. **조직 환경 설정 관리** (`manage_organization_preferences`)
    - 조직 차원의 환경 설정 관리
    - 매개변수: `org_id`, `preferences`
    - 예시: 조직의 기본 테마 및 시간대 설정 