# Grafana MCP API 기능 목록: 인시던트 관리

이 문서는 MCP(Model Context Protocol)를 통해 Grafana에서 제공할 수 있는 인시던트 관리 관련 기능들을 상세히 정리한 것입니다.

## 인시던트 관리

### 인시던트 생명주기 관리

201. **인시던트 목록 조회** (`list_incidents`)
    - 모든 인시던트 조회 및 필터링
    - 매개변수: `status`, `labels`, `time_range`, `limit`
    - 예시: 현재 진행 중인 모든 중요 인시던트 조회

202. **인시던트 생성** (`create_incident`)
    - 새 인시던트 생성
    - 매개변수: `title`, `description`, `labels`, `priority`, `owner`
    - 예시: 웹사이트 가용성 문제에 대한 인시던트 생성

203. **인시던트 상세 조회** (`get_incident`)
    - 특정 인시던트의 상세 정보 조회
    - 매개변수: `incident_id`
    - 예시: 진행 중인 인시던트의 현재 상태 및 이력 조회

204. **인시던트 업데이트** (`update_incident`)
    - 인시던트 정보 수정
    - 매개변수: `incident_id`, `title`, `description`, `labels`, `priority`, `owner`
    - 예시: 인시던트 우선순위 변경 및 라벨 추가

205. **인시던트 해결** (`resolve_incident`)
    - 인시던트를 해결됨으로 표시
    - 매개변수: `incident_id`, `resolution_notes`
    - 예시: 수행한 조치와 함께 인시던트 종료

206. **인시던트 재개** (`reopen_incident`)
    - 해결된 인시던트 재개
    - 매개변수: `incident_id`, `reason`
    - 예시: 이전에 해결된 문제가 재발생하여 인시던트 재개

207. **인시던트 이관** (`assign_incident`)
    - 인시던트를 새 담당자에게 할당
    - 매개변수: `incident_id`, `assignee`, `message`
    - 예시: 인시던트를 데이터베이스 팀으로 이관

208. **인시던트 에스컬레이션** (`escalate_incident`)
    - 인시던트 우선순위 상향 조정
    - 매개변수: `incident_id`, `new_priority`, `reason`
    - 예시: 사용자 영향이 예상보다 큰 경우 우선순위 상향

### 인시던트 활동 및 상태 관리

209. **인시던트 활동 추가** (`add_activity_to_incident`)
    - 인시던트에 활동 정보 추가
    - 매개변수: `incident_id`, `activity_type`, `description`, `user`
    - 예시: 수행한 조치에 대한 상태 업데이트 추가

210. **인시던트 활동 목록 조회** (`list_incident_activities`)
    - 인시던트 활동 기록 조회
    - 매개변수: `incident_id`, `limit`
    - 예시: 인시던트 처리 중 수행된 모든 활동 이력 조회

211. **인시던트 타임라인 생성** (`create_incident_timeline`)
    - 인시던트 타임라인 시각화
    - 매개변수: `incident_id`
    - 예시: 인시던트 발생부터 해결까지의 활동 시각화

212. **인시던트 상태 업데이트** (`update_incident_status`)
    - 인시던트 상태 변경
    - 매개변수: `incident_id`, `status`, `message`
    - 예시: 인시던트 상태를 "조사 중"에서 "완화 중"으로 변경

213. **인시던트 메모 추가** (`add_incident_note`)
    - 인시던트에 텍스트 메모 추가
    - 매개변수: `incident_id`, `note`, `user`
    - 예시: 인시던트 조사 결과에 대한 메모 추가

214. **인시던트 메모 목록 조회** (`list_incident_notes`)
    - 인시던트에 추가된 모든 메모 조회
    - 매개변수: `incident_id`
    - 예시: 인시던트에 대한 모든 메모 및 내부 논의 조회

215. **인시던트 라벨 관리** (`manage_incident_labels`)
    - 인시던트 라벨 추가/제거
    - 매개변수: `incident_id`, `labels_to_add`, `labels_to_remove`
    - 예시: 인시던트에 "데이터베이스" 라벨 추가

### 인시던트 분석 및 보고

216. **인시던트 메트릭 조회** (`get_incident_metrics`)
    - 인시던트 시간, 해결 시간 등의 메트릭 조회
    - 매개변수: `time_range`, `group_by`
    - 예시: 지난 분기 평균 해결 시간 및 인시던트 수 조회

217. **인시던트 보고서 생성** (`create_incident_report`)
    - 인시던트에 대한 사후 분석 보고서 생성
    - 매개변수: `incident_id`, `report_type`, `contributors`
    - 예시: 주요 인시던트에 대한 근본 원인 분석 보고서 생성

218. **인시던트 요약 생성** (`create_incident_summary`)
    - 인시던트 주요 정보 요약
    - 매개변수: `incident_id`
    - 예시: 이해관계자를 위한 인시던트 핵심 요약 생성

219. **유사 인시던트 검색** (`find_similar_incidents`)
    - 유사한 과거 인시던트 검색
    - 매개변수: `incident_id`, `similarity_criteria`, `time_range`
    - 예시: 동일한 서비스에서 발생한 유사한 인시던트 찾기

220. **인시던트 추세 분석** (`analyze_incident_trends`)
    - 시간에 따른 인시던트 패턴 분석
    - 매개변수: `criteria`, `time_range`, `group_by`
    - 예시: 서비스별, 월별 인시던트 발생 추세 분석

221. **근본 원인 분류** (`categorize_incident_root_causes`)
    - 인시던트 근본 원인 분류 및 통계
    - 매개변수: `time_range`, `group_by`
    - 예시: 지난 분기 인시던트 원인별 분류 및 비율 확인 