# Grafana MCP API 기능 목록: 인시던트 관리

이 문서는 MCP(Model Context Protocol)를 통해 Grafana에서 제공할 수 있는 인시던트 관리 관련 기능들을 상세히 정리한 것입니다.

## 인시던트 관리

### 인시던트 CRUD 및 라이프사이클 관리

201. **인시던트 목록 조회** (`list_incidents`)
    - 모든 인시던트 조회 및 필터링
    - 매개변수: `status`, `severity`, `service`, `created_after`, `created_before`, `limit`
    - 예시: 지난 24시간 동안 발생한 심각도 높은 인시던트 조회

202. **인시던트 생성** (`create_incident`)
    - 수동으로 새 인시던트 생성
    - 매개변수: `title`, `description`, `severity`, `service`, `tags`
    - 예시: 외부에서 감지된 문제에 대한 인시던트 생성

203. **인시던트 상세 조회** (`get_incident`)
    - 특정 인시던트의 상세 정보 조회
    - 매개변수: `incident_id`
    - 예시: 인시던트의 현재 상태, 타임라인, 할당자 조회

204. **인시던트 업데이트** (`update_incident`)
    - 인시던트 정보 업데이트
    - 매개변수: `incident_id`, `status`, `severity`, `assignee`, `summary`
    - 예시: 인시던트 심각도 조정 또는 담당자 변경

205. **인시던트 종료** (`resolve_incident`)
    - a인시던트를 해결됨으로 표시하고 종료
    - 매개변수: `incident_id`, `resolution_summary`
    - 예시: 문제 해결 후 인시던트 종료 및 요약 정보 기록

206. **인시던트 상태 변경** (`change_incident_status`)
    - 인시던트 상태 변경 (조사 중, 완화 중, 해결됨 등)
    - 매개변수: `incident_id`, `status`, `comment`
    - 예시: 인시던트 상태를 '조사 중'에서 '완화 중'으로 변경

207. **인시던트 심각도 설정** (`set_incident_severity`)
    - 인시던트 심각도 변경
    - 매개변수: `incident_id`, `severity`, `reason`
    - 예시: 추가 영향 발견 후 인시던트 심각도 상향 조정

208. **인시던트 우선순위 설정** (`set_incident_priority`)
    - 인시던트 우선순위 설정
    - 매개변수: `incident_id`, `priority`, `reason`
    - 예시: 비즈니스 영향에 따른 인시던트 우선순위 조정

209. **인시던트 담당자 할당** (`assign_incident`)
    - 인시던트 담당자 지정
    - 매개변수: `incident_id`, `assignee_id`, `message`
    - 예시: 전문 지식을 가진 엔지니어에게 인시던트 할당

210. **인시던트 라벨 관리** (`manage_incident_labels`)
    - 인시던트 라벨 추가/제거
    - 매개변수: `incident_id`, `labels_to_add`, `labels_to_remove`
    - 예시: 인시던트에 '데이터베이스', '성능' 라벨 추가

### 인시던트 관련 리소스 관리

211. **인시던트 타임라인 조회** (`get_incident_timeline`)
    - 인시던트 활동 타임라인 조회
    - 매개변수: `incident_id`
    - 예시: 인시던트 생성부터 해결까지의 모든 활동 및 상태 변경 이력 조회

212. **타임라인 이벤트 추가** (`add_timeline_event`)
    - 인시던트 타임라인에 이벤트 추가
    - 매개변수: `incident_id`, `event_type`, `description`, `metadata`
    - 예시: 주요 조사 결과 또는 조치 내용 기록

213. **인시던트 노트 목록 조회** (`list_incident_notes`)
    - 인시던트 노트 목록 조회
    - 매개변수: `incident_id`
    - 예시: 인시던트에 추가된 모든 메모 및 업데이트 조회

214. **인시던트 노트 추가** (`add_incident_note`)
    - 인시던트에 새 노트 추가
    - 매개변수: `incident_id`, `content`, `user_id`
    - 예시: 문제 원인에 대한 분석 내용 추가

215. **인시던트 노트 업데이트** (`update_incident_note`)
    - 기존 인시던트 노트 업데이트
    - 매개변수: `incident_id`, `note_id`, `content`
    - 예시: 기존 메모의 잘못된 정보 수정

216. **인시던트 노트 삭제** (`delete_incident_note`)
    - 인시던트 노트 삭제
    - 매개변수: `incident_id`, `note_id`
    - 예시: 관련 없는 메모 제거

217. **관련 알림 목록 조회** (`list_related_alerts`)
    - 인시던트와 관련된 알림 목록 조회
    - 매개변수: `incident_id`
    - 예시: 인시던트를 트리거한 모든 알림 및 현재 상태 조회

218. **관련 알림 연결** (`link_alert_to_incident`)
    - 기존 알림을 인시던트와 연결
    - 매개변수: `incident_id`, `alert_id`
    - 예시: 관련된 추가 알림을 인시던트에 연결

219. **관련 알림 연결 해제** (`unlink_alert_from_incident`)
    - 인시던트에서 알림 연결 해제
    - 매개변수: `incident_id`, `alert_id`, `reason`
    - 예시: 관련 없는 알림을 인시던트에서 분리

220. **관련 대시보드 관리** (`manage_incident_dashboards`)
    - 인시던트 관련 대시보드 관리
    - 매개변수: `incident_id`, `dashboards_to_add`, `dashboards_to_remove`
    - 예시: 인시던트 분석을 위한 관련 대시보드 연결

221. **인시던트 스냅샷 생성** (`create_incident_snapshot`)
    - 인시던트 관련 대시보드 및 메트릭 스냅샷 생성
    - 매개변수: `incident_id`, `dashboard_uids`, `time_range`
    - 예시: 인시던트 발생 시점의 시스템 상태 스냅샷 저장

### 인시던트 커뮤니케이션 및 협업

222. **인시던트 알림 전송** (`send_incident_notification`)
    - 인시던트 관련 알림 전송
    - 매개변수: `incident_id`, `channels`, `message`
    - 예시: 운영팀에 인시던트 상태 업데이트 알림 전송

223. **상태 업데이트 게시** (`post_status_update`)
    - 인시던트 상태 업데이트 게시
    - 매개변수: `incident_id`, `status`, `message`, `notify`
    - 예시: 인시던트 해결 진행 상황에 대한 정기 업데이트 게시

224. **인시던트 에스컬레이션** (`escalate_incident`)
    - 인시던트 에스컬레이션
    - 매개변수: `incident_id`, `escalation_level`, `reason`, `notify_users`
    - 예시: 해결 지연 시 상위 관리자에게 인시던트 에스컬레이션

225. **인시던트 회의 생성** (`create_incident_meeting`)
    - 인시던트 대응 회의 생성
    - 매개변수: `incident_id`, `meeting_type`, `scheduled_time`, `participants`
    - 예시: 심각한 인시던트에 대한 긴급 대응 회의 소집

226. **인시던트 채팅방 관리** (`manage_incident_chat`)
    - 인시던트 전용 채팅방 관리
    - 매개변수: `incident_id`, `action`, `users_to_add`, `platform`
    - 예시: Slack에 인시던트 전용 채널 생성 및 관련자 초대

227. **외부 티켓 연동** (`link_external_ticket`)
    - 외부 티켓 시스템과 인시던트 연동
    - 매개변수: `incident_id`, `ticket_system`, `ticket_id`, `url`
    - 예시: JIRA 이슈를 Grafana 인시던트와 연결

228. **외부 티켓 생성** (`create_external_ticket`)
    - 인시던트에 대한 외부 티켓 생성
    - 매개변수: `incident_id`, `ticket_system`, `ticket_data`
    - 예시: Grafana 인시던트 정보를 바탕으로 ServiceNow 티켓 생성

### 인시던트 분석 및 보고

229. **인시던트 메트릭 조회** (`get_incident_metrics`)
    - 인시던트 관련 메트릭 조회
    - 매개변수: `incident_id`, `metrics_type`
    - 예시: 인시던트 감지부터 해결까지 소요된 시간 조회

230. **사후 분석(Postmortem) 생성** (`create_postmortem`)
    - 인시던트 사후 분석 문서 생성
    - 매개변수: `incident_id`, `template`, `assignee`
    - 예시: 표준 템플릿을 사용하여 인시던트 사후 분석 문서 초안 생성

231. **사후 분석 업데이트** (`update_postmortem`)
    - 인시던트 사후 분석 문서 업데이트
    - 매개변수: `incident_id`, `content`, `status`
    - 예시: 원인 분석 및 예방 조치 정보 추가

232. **사후 분석 조회** (`get_postmortem`)
    - 인시던트 사후 분석 문서 조회
    - 매개변수: `incident_id`
    - 예시: 완료된 사후 분석 문서 검토

233. **인시던트 보고서 생성** (`generate_incident_report`)
    - 인시던트 요약 보고서 생성
    - 매개변수: `incident_id`, `report_type`, `format`
    - 예시: 경영진을 위한 인시던트 요약 보고서 생성

234. **유사 인시던트 검색** (`find_similar_incidents`)
    - 유사한 과거 인시던트 검색
    - 매개변수: `incident_id`, `time_range`, `max_results`
    - 예시: 유사한 증상을 보인 과거 인시던트 조회

235. **근본 원인 분석 추가** (`add_root_cause_analysis`)
    - 인시던트 근본 원인 분석 정보 추가
    - 매개변수: `incident_id`, `root_causes`, `contributing_factors`
    - 예시: 인시던트의 기술적 원인 및 프로세스 요인 기록

236. **개선 항목 생성** (`create_improvement_items`)
    - 인시던트 사후 개선 항목 생성
    - 매개변수: `incident_id`, `items`, `assignees`
    - 예시: 인시던트 재발 방지를 위한 작업 항목 생성

237. **개선 항목 진행 상황 업데이트** (`update_improvement_item_status`)
    - 개선 항목 상태 업데이트
    - 매개변수: `item_id`, `status`, `comment`
    - 예시: 완료된 개선 작업 항목 상태 업데이트

### 인시던트 설정 및 템플릿

238. **인시던트 템플릿 목록 조회** (`list_incident_templates`)
    - 인시던트 템플릿 목록 조회
    - 매개변수: `limit`, `category`
    - 예시: 데이터베이스 관련 인시던트 템플릿 조회

239. **인시던트 템플릿 생성** (`create_incident_template`)
    - 새 인시던트 템플릿 생성
    - 매개변수: `name`, `description`, `severity`, `tasks`, `playbook`, `tags`
    - 예시: 네트워크 장애 인시던트를 위한 표준 대응 템플릿 생성

240. **인시던트 템플릿 업데이트** (`update_incident_template`)
    - 기존 인시던트 템플릿 수정
    - 매개변수: `template_id`, `name`, `description`, `severity`, `tasks`, `playbook`
    - 예시: 기존 템플릿에 새로운 대응 절차 추가

241. **인시던트 템플릿 삭제** (`delete_incident_template`)
    - 인시던트 템플릿 삭제
    - 매개변수: `template_id`
    - 예시: 더 이상 관련 없는 템플릿 제거

242. **인시던트 템플릿 적용** (`apply_incident_template`)
    - 기존 인시던트에 템플릿 적용
    - 매개변수: `incident_id`, `template_id`
    - 예시: 표준화된 대응 절차를 진행 중인 인시던트에 적용

243. **플레이북 목록 조회** (`list_playbooks`)
    - 인시던트 대응 플레이북 목록 조회
    - 매개변수: `category`, `tags`
    - 예시: 특정 유형의 장애에 대한 대응 절차 조회

244. **플레이북 생성** (`create_playbook`)
    - 새 인시던트 대응 플레이북 생성
    - 매개변수: `name`, `description`, `content`, `tags`
    - 예시: 데이터베이스 성능 저하 문제에 대한 체계적인 대응 절차 문서화

245. **플레이북 업데이트** (`update_playbook`)
    - 기존 플레이북 수정
    - 매개변수: `playbook_id`, `name`, `description`, `content`
    - 예시: 새로운 모범 사례를 반영하여 플레이북 업데이트

246. **플레이북 삭제** (`delete_playbook`)
    - 플레이북 삭제
    - 매개변수: `playbook_id`
    - 예시: 더 이상 관련 없는 플레이북 제거

247. **인시던트에 플레이북 연결** (`link_playbook_to_incident`)
    - 인시던트에 관련 플레이북 연결
    - 매개변수: `incident_id`, `playbook_id`
    - 예시: 진행 중인 인시던트에 관련 대응 절차 플레이북 연결

248. **체크리스트 항목 관리** (`manage_checklist_items`)
    - 인시던트 체크리스트 항목 관리
    - 매개변수: `incident_id`, `items_to_add`, `items_to_remove`, `items_to_update`
    - 예시: 인시던트 해결을 위한 필수 단계 체크리스트 구성

249. **체크리스트 항목 완료 처리** (`complete_checklist_item`)
    - 체크리스트 항목 완료 처리
    - 매개변수: `incident_id`, `item_id`, `completed_by`, `comment`
    - 예시: 데이터베이스 재시작 단계 완료 표시

250. **알림 정책 구성** (`configure_notification_policy`)
    - 인시던트 알림 정책 구성
    - 매개변수: `severity_levels`, `notification_channels`, `schedules`
    - 예시: 심각도별 다른 알림 채널 및 알림 대상자 구성 