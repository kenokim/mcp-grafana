# Grafana MCP API 기능 목록: 대시보드 및 알림 관리

이 문서는 MCP(Model Context Protocol)를 통해 Grafana에서 제공할 수 있는 대시보드 및 알림 관리 관련 기능들을 상세히 정리한 것입니다.

## 대시보드 관리

### 대시보드 CRUD 및 버전 관리

301. **대시보드 목록 조회** (`list_dashboards`)
    - 대시보드 목록 조회 및 필터링
    - 매개변수: `folder_id`, `query`, `tags`, `starred`, `limit`
    - 예시: 특정 태그를 가진 모든 대시보드 조회

302. **대시보드 생성** (`create_dashboard`)
    - 새 대시보드 생성
    - 매개변수: `dashboard_json`, `folder_id`, `overwrite`, `message`
    - 예시: 시스템 모니터링을 위한 새 대시보드 생성

303. **대시보드 상세 조회** (`get_dashboard`)
    - 특정 대시보드의 상세 정보 조회
    - 매개변수: `dashboard_uid`
    - 예시: 대시보드 패널 및 설정 정보 조회

304. **대시보드 업데이트** (`update_dashboard`)
    - 기존 대시보드 수정
    - 매개변수: `dashboard_uid`, `dashboard_json`, `overwrite`, `message`
    - 예시: 대시보드에 새 패널 추가

305. **대시보드 삭제** (`delete_dashboard`)
    - 대시보드 삭제
    - 매개변수: `dashboard_uid`
    - 예시: 더 이상 필요 없는 대시보드 제거

306. **대시보드 버전 목록 조회** (`list_dashboard_versions`)
    - 대시보드의 이전 버전 목록 조회
    - 매개변수: `dashboard_uid`, `limit`
    - 예시: 대시보드의 변경 이력 확인

307. **대시보드 버전 상세 조회** (`get_dashboard_version`)
    - 특정 버전의 대시보드 조회
    - 매개변수: `dashboard_uid`, `version`
    - 예시: 특정 시점의 대시보드 구성 확인

308. **대시보드 버전 복원** (`restore_dashboard_version`)
    - 이전 버전의 대시보드로 복원
    - 매개변수: `dashboard_uid`, `version`
    - 예시: 잘못된 변경 사항 롤백

309. **대시보드 버전 비교** (`compare_dashboard_versions`)
    - 두 대시보드 버전 간의 차이점 비교
    - 매개변수: `dashboard_uid`, `base_version`, `new_version`
    - 예시: 변경된 패널 및 쿼리 확인

310. **대시보드 복제** (`clone_dashboard`)
    - 기존 대시보드를 복제하여 새 대시보드 생성
    - 매개변수: `dashboard_uid`, `new_title`, `folder_id`
    - 예시: 템플릿으로 활용하기 위한 대시보드 복제

### 대시보드 템플릿 및 변수 관리

311. **대시보드 템플릿 목록 조회** (`list_dashboard_templates`)
    - 사용 가능한 대시보드 템플릿 목록 조회
    - 매개변수: `category`, `tags`
    - 예시: 애플리케이션 모니터링 템플릿 조회

312. **대시보드 템플릿 적용** (`apply_dashboard_template`)
    - 템플릿을 적용하여 새 대시보드 생성
    - 매개변수: `template_id`, `variables`, `folder_id`
    - 예시: 서비스 모니터링 템플릿으로 새 대시보드 생성

313. **대시보드 변수 목록 조회** (`list_dashboard_variables`)
    - 대시보드에 정의된 변수 목록 조회
    - 매개변수: `dashboard_uid`
    - 예시: 대시보드에서 사용 중인 모든 템플릿 변수 조회

314. **대시보드 변수 추가** (`add_dashboard_variable`)
    - 대시보드에 새 변수 추가
    - 매개변수: `dashboard_uid`, `name`, `type`, `query`, `options`
    - 예시: 환경 선택을 위한 드롭다운 변수 추가

315. **대시보드 변수 업데이트** (`update_dashboard_variable`)
    - 기존 대시보드 변수 수정
    - 매개변수: `dashboard_uid`, `variable_id`, `name`, `type`, `query`, `options`
    - 예시: 변수의 기본값 변경

316. **대시보드 변수 삭제** (`delete_dashboard_variable`)
    - 대시보드에서 변수 제거
    - 매개변수: `dashboard_uid`, `variable_id`
    - 예시: 더 이상 사용하지 않는 변수 제거

317. **대시보드 변수값 조회** (`get_dashboard_variable_values`)
    - 대시보드 변수의 가능한 값 목록 조회
    - 매개변수: `dashboard_uid`, `variable_id`
    - 예시: 사용 가능한 모든 서비스 이름 조회

318. **대시보드 변수 설정 적용** (`apply_dashboard_variable_settings`)
    - 대시보드 변수의 현재 값 설정
    - 매개변수: `dashboard_uid`, `variables`
    - 예시: 특정 환경 및 시간 범위로 대시보드 구성

### 대시보드 폴더 관리

319. **폴더 목록 조회** (`list_folders`)
    - 모든 대시보드 폴더 조회
    - 매개변수: `limit`, `page`
    - 예시: 모든 폴더 계층 구조 조회

320. **폴더 생성** (`create_folder`)
    - 새 대시보드 폴더 생성
    - 매개변수: `title`, `uid`
    - 예시: 마이크로서비스별 대시보드를 위한 폴더 생성

321. **폴더 상세 조회** (`get_folder`)
    - 특정 폴더의 상세 정보 조회
    - 매개변수: `folder_uid`
    - 예시: 폴더 메타데이터 및 권한 조회

322. **폴더 업데이트** (`update_folder`)
    - 기존 폴더 정보 수정
    - 매개변수: `folder_uid`, `title`
    - 예시: 폴더 이름 변경

323. **폴더 삭제** (`delete_folder`)
    - 폴더 및 포함된 대시보드 삭제
    - 매개변수: `folder_uid`
    - 예시: 사용하지 않는 프로젝트 폴더 정리

324. **폴더 내 대시보드 목록 조회** (`list_dashboards_in_folder`)
    - 특정 폴더에 포함된 대시보드 목록 조회
    - 매개변수: `folder_uid`
    - 예시: 폴더 내 모든 대시보드 조회

325. **폴더 권한 조회** (`get_folder_permissions`)
    - 폴더 접근 권한 조회
    - 매개변수: `folder_uid`
    - 예시: 폴더에 대한 사용자 및 팀 권한 확인

326. **폴더 권한 설정** (`update_folder_permissions`)
    - 폴더의 접근 권한 설정
    - 매개변수: `folder_uid`, `permissions`
    - 예시: 특정 팀에 폴더 편집 권한 부여

327. **폴더 이동** (`move_folder`)
    - 폴더를 다른 폴더로 이동
    - 매개변수: `folder_uid`, `target_folder_uid`
    - 예시: 폴더 계층 구조 재구성

### 대시보드 패널 및 데이터 관리

328. **패널 추가** (`add_panel`)
    - 대시보드에 새 패널 추가
    - 매개변수: `dashboard_uid`, `panel_json`, `position`
    - 예시: CPU 사용량 시각화 패널 추가

329. **패널 업데이트** (`update_panel`)
    - 기존 패널 수정
    - 매개변수: `dashboard_uid`, `panel_id`, `panel_json`
    - 예시: 패널의 시각화 유형 변경

330. **패널 삭제** (`delete_panel`)
    - 대시보드에서 패널 제거
    - 매개변수: `dashboard_uid`, `panel_id`
    - 예시: 불필요한 패널 제거

331. **패널 복제** (`clone_panel`)
    - 기존 패널을 복제하여 새 패널 생성
    - 매개변수: `dashboard_uid`, `panel_id`, `position`
    - 예시: 유사한 메트릭을 위한 패널 복제

332. **패널 이동** (`move_panel`)
    - 패널 위치 변경
    - 매개변수: `dashboard_uid`, `panel_id`, `position`
    - 예시: 관련 패널 그룹화를 위한 재배치

333. **패널 데이터 조회** (`get_panel_data`)
    - 패널에 표시된 데이터 조회
    - 매개변수: `dashboard_uid`, `panel_id`, `time_range`, `variables`
    - 예시: 패널에 표시된 원시 데이터 확인

334. **패널 쿼리 수정** (`update_panel_query`)
    - 패널의 데이터 쿼리 수정
    - 매개변수: `dashboard_uid`, `panel_id`, `query`, `datasource`
    - 예시: 쿼리 필터 조건 변경

335. **패널 옵션 수정** (`update_panel_options`)
    - 패널의 디스플레이 옵션 수정
    - 매개변수: `dashboard_uid`, `panel_id`, `options`
    - 예시: 패널 단위 및 임계값 변경

336. **패널 이미지 생성** (`get_panel_image`)
    - 패널의 렌더링된 이미지 생성
    - 매개변수: `dashboard_uid`, `panel_id`, `width`, `height`, `time_range`
    - 예시: 보고서용 패널 이미지 생성

### 스냅샷 및 공유

337. **대시보드 스냅샷 생성** (`create_dashboard_snapshot`)
    - 대시보드의 현재 상태 스냅샷 생성
    - 매개변수: `dashboard_uid`, `name`, `expires`
    - 예시: 인시던트 조사를 위한 대시보드 상태 저장

338. **대시보드 스냅샷 목록 조회** (`list_dashboard_snapshots`)
    - 스냅샷 목록 조회
    - 매개변수: `limit`, `query`
    - 예시: 특정 기간에 생성된 스냅샷 조회

339. **대시보드 스냅샷 조회** (`get_dashboard_snapshot`)
    - 특정 스냅샷의 상세 정보 조회
    - 매개변수: `snapshot_id`
    - 예시: 저장된 대시보드 스냅샷 데이터 조회

340. **대시보드 스냅샷 삭제** (`delete_dashboard_snapshot`)
    - 스냅샷 삭제
    - 매개변수: `snapshot_id`
    - 예시: 더 이상 필요 없는 스냅샷 제거

341. **대시보드 공유 링크 생성** (`create_dashboard_share_link`)
    - 대시보드 공유 링크 생성
    - 매개변수: `dashboard_uid`, `time_range`, `variables`, `expires`
    - 예시: 특정 설정이 적용된 대시보드 링크 생성

342. **공유 링크 목록 조회** (`list_share_links`)
    - 생성된 공유 링크 목록 조회
    - 매개변수: `dashboard_uid`
    - 예시: 대시보드에 대해 생성된 모든 공유 링크 조회

343. **공유 링크 삭제** (`delete_share_link`)
    - 공유 링크 삭제
    - 매개변수: `link_id`
    - 예시: 만료된 공유 링크 제거

344. **대시보드 내보내기** (`export_dashboard`)
    - 대시보드 JSON 내보내기
    - 매개변수: `dashboard_uid`, `format`
    - 예시: 버전 관리 시스템에 저장하기 위한 대시보드 내보내기

345. **대시보드 가져오기** (`import_dashboard`)
    - JSON에서 대시보드 가져오기
    - 매개변수: `dashboard_json`, `folder_id`, `overwrite`
    - 예시: 기존 대시보드 구성 가져오기

## 알림 관리

### 알림 규칙 관리

346. **알림 규칙 목록 조회** (`list_alert_rules`)
    - 모든 알림 규칙 조회 및 필터링
    - 매개변수: `folder_uid`, `dashboard_uid`, `group_name`, `state`
    - 예시: 특정 대시보드의 모든 알림 규칙 조회

347. **알림 규칙 생성** (`create_alert_rule`)
    - 새 알림 규칙 생성
    - 매개변수: `name`, `query`, `condition`, `folder_uid`, `evaluator`, `annotations`, `labels`
    - 예시: CPU 사용량이 90% 이상인 경우 알림 생성

348. **알림 규칙 상세 조회** (`get_alert_rule`)
    - 특정 알림 규칙의 상세 정보 조회
    - 매개변수: `alert_uid`
    - 예시: 알림 규칙의 쿼리 및 조건 확인

349. **알림 규칙 업데이트** (`update_alert_rule`)
    - 기존 알림 규칙 수정
    - 매개변수: `alert_uid`, `name`, `query`, `condition`, `evaluator`, `annotations`, `labels`
    - 예시: 알림 임계값 조정

350. **알림 규칙 삭제** (`delete_alert_rule`)
    - 알림 규칙 삭제
    - 매개변수: `alert_uid`
    - 예시: 더 이상 필요 없는 알림 제거

351. **알림 규칙 일시 중지** (`pause_alert_rule`)
    - 알림 규칙 평가 일시 중지
    - 매개변수: `alert_uid`
    - 예시: 유지보수 기간 동안 알림 중지

352. **알림 규칙 재개** (`resume_alert_rule`)
    - 일시 중지된 알림 규칙 재개
    - 매개변수: `alert_uid`
    - 예시: 유지보수 완료 후 알림 재활성화

353. **알림 규칙 테스트** (`test_alert_rule`)
    - 알림 규칙 평가 테스트
    - 매개변수: `rule_json`, `data`
    - 예시: 배포 전 알림 규칙 동작 확인

354. **알림 규칙 그룹 생성** (`create_alert_rule_group`)
    - 알림 규칙 그룹 생성
    - 매개변수: `name`, `folder_uid`, `interval`
    - 예시: 관련 알림을 그룹화하여 관리

355. **알림 규칙 그룹 업데이트** (`update_alert_rule_group`)
    - 알림 규칙 그룹 수정
    - 매개변수: `group_uid`, `name`, `interval`
    - 예시: 알림 그룹의 평가 간격 조정

### 알림 인스턴스 및 상태 관리

356. **알림 인스턴스 목록 조회** (`list_alert_instances`)
    - 현재 활성화된 알림 인스턴스 조회
    - 매개변수: `rule_uid`, `state`
    - 예시: 현재 발생 중인 모든 알림 조회

357. **알림 인스턴스 상세 조회** (`get_alert_instance`)
    - 특정 알림 인스턴스의 상세 정보 조회
    - 매개변수: `instance_id`
    - 예시: 특정 알림에 대한 라벨 및 값 조회

358. **알림 상태 이력 조회** (`get_alert_state_history`)
    - 알림 상태 변경 이력 조회
    - 매개변수: `rule_uid`, `time_range`
    - 예시: 알림 발생 및 해결 타임라인 확인

359. **알림 인스턴스 무음 처리** (`silence_alert_instance`)
    - 특정 알림 인스턴스 무음 처리
    - 매개변수: `instance_id`, `duration`, `comment`
    - 예시: 처리 중인 알림 일시적 무음 처리

360. **알림 무음 처리 목록 조회** (`list_alert_silences`)
    - 모든 무음 처리된 알림 조회
    - 매개변수: `matchers`, `state`
    - 예시: 현재 활성화된 모든 무음 처리 조회

361. **알림 무음 처리 생성** (`create_alert_silence`)
    - 새 알림 무음 처리 규칙 생성
    - 매개변수: `matchers`, `starts_at`, `ends_at`, `comment`, `created_by`
    - 예시: 계획된 유지보수 기간 동안 특정 서비스에 대한 알림 무음 처리

362. **알림 무음 처리 취소** (`delete_alert_silence`)
    - 무음 처리 규칙 취소
    - 매개변수: `silence_id`
    - 예시: 유지보수가 예정보다 일찍 완료된 경우 무음 처리 취소

363. **알림 상태 요약 조회** (`get_alert_summary`)
    - 알림 상태 요약 통계 조회
    - 매개변수: `folder_uid`, `dashboard_uid`
    - 예시: 폴더별 활성/해결된 알림 개수 확인

### 알림 알림(Notification) 관리

364. **알림 수신자 목록 조회** (`list_alert_receivers`)
    - 구성된 모든 알림 수신자 조회
    - 매개변수: `name`
    - 예시: 모든 이메일 및 Slack 알림 수신자 조회

365. **알림 수신자 생성** (`create_alert_receiver`)
    - 새 알림 수신자 구성 생성
    - 매개변수: `name`, `type`, `settings`
    - 예시: 새 Slack 채널에 알림을 보내기 위한 수신자 생성

366. **알림 수신자 상세 조회** (`get_alert_receiver`)
    - 특정 알림 수신자의 상세 정보 조회
    - 매개변수: `receiver_name`
    - 예시: 이메일 알림 설정 확인

367. **알림 수신자 업데이트** (`update_alert_receiver`)
    - 기존 알림 수신자 구성 수정
    - 매개변수: `receiver_name`, `type`, `settings`
    - 예시: 알림 이메일 주소 업데이트

368. **알림 수신자 삭제** (`delete_alert_receiver`)
    - 알림 수신자 제거
    - 매개변수: `receiver_name`
    - 예시: 더 이상 사용하지 않는 Webhook 수신자 제거

369. **알림 정책 목록 조회** (`list_notification_policies`)
    - 알림 라우팅 정책 조회
    - 매개변수: `none`
    - 예시: 현재 구성된 알림 전달 정책 확인

370. **알림 정책 업데이트** (`update_notification_policies`)
    - 알림 라우팅 정책 수정
    - 매개변수: `policy_tree`
    - 예시: 새 라우팅 규칙 추가 및 기본 수신자 변경

371. **알림 템플릿 목록 조회** (`list_notification_templates`)
    - 알림 메시지 템플릿 조회
    - 매개변수: `none`
    - 예시: 사용 가능한 모든 알림 템플릿 조회

372. **알림 템플릿 생성** (`create_notification_template`)
    - 새 알림 메시지 템플릿 생성
    - 매개변수: `name`, `template`
    - 예시: 특정 형식의 알림 메시지 템플릿 생성

373. **알림 템플릿 업데이트** (`update_notification_template`)
    - 기존 알림 템플릿 수정
    - 매개변수: `name`, `template`
    - 예시: 알림 템플릿에 추가 정보 포함

374. **알림 템플릿 삭제** (`delete_notification_template`)
    - 알림 템플릿 제거
    - 매개변수: `name`
    - 예시: 사용하지 않는 템플릿 정리

375. **알림 메시지 테스트** (`test_notification`)
    - 알림 메시지 전송 테스트
    - 매개변수: `receiver_name`, `annotations`, `labels`
    - 예시: 새 수신자 구성 확인을 위한 테스트 알림 전송

376. **알림 이력 조회** (`get_notification_history`)
    - 알림 전송 이력 조회
    - 매개변수: `time_range`, `receiver_name`
    - 예시: 특정 수신자에게 전송된 모든 알림 확인 