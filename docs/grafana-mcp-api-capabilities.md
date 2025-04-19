# Grafana MCP API 기능 목록

이 문서는 MCP(Model Context Protocol)를 통해 Grafana에서 제공할 수 있는 기능들을 상세히 정리한 것입니다. 각 기능은 MCP 도구로 구현될 수 있으며, AI 모델이 Grafana 생태계와 더 효과적으로 상호작용할 수 있게 합니다.

## 목차

1. [데이터 시각화 및 대시보드](#데이터-시각화-및-대시보드)
2. [데이터 소스 관리](#데이터-소스-관리)
3. [쿼리 및 변환](#쿼리-및-변환)
4. [알림 및 알림 관리](#알림-및-알림-관리)
5. [로깅 및 모니터링](#로깅-및-모니터링)
6. [트레이싱 및 프로파일링](#트레이싱-및-프로파일링)
7. [인시던트 관리](#인시던트-관리)
8. [사용자 및 팀 관리](#사용자-및-팀-관리)
9. [권한 및 접근 제어](#권한-및-접근-제어)
10. [환경 설정 관리](#환경-설정-관리)
11. [플러그인 관리](#플러그인-관리)
12. [API 및 통합](#api-및-통합)

## 데이터 시각화 및 대시보드

### 대시보드 관리

1. **대시보드 검색** (`search_dashboards`)
   - 다양한 필터(태그, 폴더, 제목, 별표 등)를 사용하여 대시보드 검색
   - 매개변수: `query`, `tags`, `folder_ids`, `starred`, `limit`, `page`
   - 예시: "production" 태그가 있는 모든 대시보드 검색

2. **대시보드 가져오기** (`get_dashboard_by_uid`)
   - UID를 기반으로 대시보드 상세 정보 조회
   - 매개변수: `uid`
   - 예시: "abc123xyz" UID를 가진 대시보드의 패널, 변수, 설정 조회

3. **대시보드 생성** (`create_dashboard`)
   - 새 대시보드 생성
   - 매개변수: `dashboard_json`, `folder_id`, `overwrite`
   - 예시: 특정 폴더에 3개의 패널이 있는 새 대시보드 생성

4. **대시보드 업데이트** (`update_dashboard`)
   - 기존 대시보드 수정
   - 매개변수: `dashboard_json`, `overwrite`, `message`
   - 예시: 기존 대시보드에 새 패널 추가, 타임레인지 변경

5. **대시보드 삭제** (`delete_dashboard`)
   - UID로 대시보드 삭제
   - 매개변수: `uid`
   - 예시: 특정 UID의 대시보드 삭제

6. **대시보드 버전 관리** (`list_dashboard_versions`)
   - 대시보드의 버전 기록 조회
   - 매개변수: `dashboard_id`, `limit`
   - 예시: 지난 10개 버전의 변경 내역 조회

7. **대시보드 버전 복원** (`restore_dashboard_version`)
   - 이전 버전으로 대시보드 복원
   - 매개변수: `dashboard_id`, `version`
   - 예시: 대시보드를 3일 전 버전으로 복원

8. **대시보드 권한 설정** (`update_dashboard_permissions`)
   - 대시보드에 대한 권한 구성
   - 매개변수: `dashboard_id`, `permissions`
   - 예시: 특정 팀에 대시보드 편집 권한 부여

9. **대시보드 비교** (`compare_dashboard_versions`)
   - 두 버전의 대시보드 차이점 확인
   - 매개변수: `dashboard_id`, `base_version`, `new_version`
   - 예시: 현재 버전과 이전 버전 간의 패널 변경 확인

10. **대시보드 스냅샷 생성** (`create_dashboard_snapshot`)
    - 현재 대시보드 상태의 공유 가능한 스냅샷 생성
    - 매개변수: `dashboard_json`, `expires`, `external`, `key`
    - 예시: 30일 동안 유효한 대시보드 스냅샷 생성

11. **대시보드 스냅샷 가져오기** (`get_dashboard_snapshot`)
    - 스냅샷 키로 대시보드 스냅샷 조회
    - 매개변수: `key`
    - 예시: 공유된 스냅샷 키로 대시보드 데이터 조회

12. **대시보드 스냅샷 삭제** (`delete_dashboard_snapshot`)
    - 키로 대시보드 스냅샷 삭제
    - 매개변수: `key`
    - 예시: 특정 스냅샷 삭제

13. **대시보드 태그 가져오기** (`get_dashboard_tags`)
    - 시스템에서 사용 중인 모든 태그 조회
    - 매개변수: `none`
    - 예시: 태그 클라우드 생성용 모든 태그 조회

14. **대시보드 즐겨찾기 설정** (`star_dashboard`)
    - 대시보드를 즐겨찾기로 설정
    - 매개변수: `dashboard_id`
    - 예시: 자주 사용하는 대시보드를 즐겨찾기에 추가

15. **대시보드 즐겨찾기 해제** (`unstar_dashboard`)
    - 대시보드 즐겨찾기 해제
    - 매개변수: `dashboard_id`
    - 예시: 더 이상 필요하지 않은 대시보드 즐겨찾기 해제

### 패널 관리

16. **패널 생성** (`create_panel`)
    - 대시보드에 새 패널 추가
    - 매개변수: `dashboard_id`, `panel_json`
    - 예시: 대시보드에 새 시계열 그래프 패널 추가

17. **패널 업데이트** (`update_panel`)
    - 기존 패널 수정
    - 매개변수: `dashboard_id`, `panel_id`, `panel_json`
    - 예시: 패널의 데이터 소스 또는 쿼리 변경

18. **패널 복제** (`clone_panel`)
    - 기존 패널 복제
    - 매개변수: `dashboard_id`, `panel_id`
    - 예시: 기존 패널을 복제하여 유사한 새 패널 생성

19. **패널 삭제** (`delete_panel`)
    - 대시보드에서 패널 제거
    - 매개변수: `dashboard_id`, `panel_id`
    - 예시: 불필요한 패널 삭제

20. **패널 이동** (`move_panel`)
    - 대시보드 내에서 패널 위치 변경
    - 매개변수: `dashboard_id`, `panel_id`, `grid_pos`
    - 예시: 패널을 좌측 상단으로 이동

21. **패널 크기 조정** (`resize_panel`)
    - 패널 크기 변경
    - 매개변수: `dashboard_id`, `panel_id`, `width`, `height`
    - 예시: 패널을 전체 너비로 확장

22. **패널 옵션 설정** (`set_panel_options`)
    - 패널 디스플레이 옵션 구성
    - 매개변수: `dashboard_id`, `panel_id`, `options`
    - 예시: 패널 범례 위치, 색상 구성표 변경

23. **패널 알림 구성** (`configure_panel_alerts`)
    - 패널에 대한 알림 규칙 설정
    - 매개변수: `dashboard_id`, `panel_id`, `alert_config`
    - 예시: CPU 사용량이 90% 초과 시 알림 설정

24. **패널 쿼리 변경** (`update_panel_queries`)
    - 패널 데이터 쿼리 수정
    - 매개변수: `dashboard_id`, `panel_id`, `queries`
    - 예시: 프로메테우스 쿼리 매개변수 조정

25. **패널 시각화 변경** (`change_panel_visualization`)
    - 패널 시각화 유형 변경
    - 매개변수: `dashboard_id`, `panel_id`, `visualization_type`
    - 예시: 라인 그래프에서 히트맵으로 변경

### 폴더 관리

26. **폴더 생성** (`create_folder`)
    - 새 대시보드 폴더 생성
    - 매개변수: `title`
    - 예시: "프로덕션 모니터링" 폴더 생성

27. **폴더 가져오기** (`get_folder`)
    - ID 또는 UID로 폴더 정보 조회
    - 매개변수: `folder_uid`
    - 예시: 특정 폴더의 상세 정보 조회

28. **폴더 업데이트** (`update_folder`)
    - 폴더 속성 업데이트
    - 매개변수: `folder_uid`, `title`, `description`
    - 예시: 폴더 제목과 설명 변경

29. **폴더 삭제** (`delete_folder`)
    - 폴더와 해당 콘텐츠 삭제
    - 매개변수: `folder_uid`
    - 예시: 더 이상 필요하지 않은 폴더 삭제

30. **폴더 권한 가져오기** (`get_folder_permissions`)
    - 폴더에 설정된 권한 조회
    - 매개변수: `folder_uid`
    - 예시: 특정 폴더에 설정된 팀 및 사용자 권한 조회

31. **폴더 권한 업데이트** (`update_folder_permissions`)
    - 폴더에 대한 권한 구성 변경
    - 매개변수: `folder_uid`, `permissions`
    - 예시: 새 팀에 폴더 읽기 권한 부여

32. **폴더 내 대시보드 나열** (`list_folder_dashboards`)
    - 특정 폴더 내 모든 대시보드 조회
    - 매개변수: `folder_id`
    - 예시: "네트워크 모니터링" 폴더의 모든 대시보드 조회

33. **폴더 목록 가져오기** (`list_folders`)
    - 모든 폴더 조회
    - 매개변수: `none`
    - 예시: 모든 폴더의 계층 구조 보기

### 플레이리스트 관리

34. **플레이리스트 생성** (`create_playlist`)
    - 여러 대시보드를 순환 표시하는 플레이리스트 생성
    - 매개변수: `name`, `interval`, `items`
    - 예시: 5분 간격으로 3개 모니터링 대시보드 순환 재생

35. **플레이리스트 가져오기** (`get_playlist`)
    - ID로 플레이리스트 상세 정보 조회
    - 매개변수: `playlist_id`
    - 예시: 특정 플레이리스트의 항목 및 간격 확인

36. **플레이리스트 업데이트** (`update_playlist`)
    - 기존 플레이리스트 수정
    - 매개변수: `playlist_id`, `name`, `interval`, `items`
    - 예시: 플레이리스트에 새 대시보드 추가

37. **플레이리스트 삭제** (`delete_playlist`)
    - 플레이리스트 삭제
    - 매개변수: `playlist_id`
    - 예시: 불필요한 플레이리스트 삭제

38. **플레이리스트 목록 가져오기** (`list_playlists`)
    - 모든 플레이리스트 조회
    - 매개변수: `none`
    - 예시: 사용 가능한 모든 플레이리스트 나열

39. **플레이리스트 시작** (`start_playlist`)
    - 플레이리스트 재생 시작
    - 매개변수: `playlist_id`, `mode`
    - 예시: 전체 화면 모드로 플레이리스트 시작

### 주석 관리

40. **주석 추가** (`create_annotation`)
    - 대시보드에 이벤트 주석 추가
    - 매개변수: `dashboard_id`, `panel_id`, `time`, `text`, `tags`
    - 예시: 배포 시점 표시하는 주석 추가

41. **주석 가져오기** (`get_annotations`)
    - 시간 범위 내 주석 조회
    - 매개변수: `dashboard_id`, `panel_id`, `from`, `to`, `tags`
    - 예시: 지난 24시간 내 모든 주석 조회

42. **주석 업데이트** (`update_annotation`)
    - 기존 주석 수정
    - 매개변수: `annotation_id`, `text`, `tags`
    - 예시: 주석 텍스트 내용 및 태그 업데이트

43. **주석 삭제** (`delete_annotation`)
    - 주석 제거
    - 매개변수: `annotation_id`
    - 예시: 더 이상 관련 없는 주석 삭제

44. **태그 기반 주석 가져오기** (`get_annotations_by_tags`)
    - 특정 태그가 있는 주석 조회
    - 매개변수: `tags`, `from`, `to`
    - 예시: "deployment" 태그가 있는 모든 주석 찾기

45. **주석 태그 가져오기** (`get_annotation_tags`)
    - 사용된 모든 주석 태그 조회
    - 매개변수: `none`
    - 예시: 주석에 사용된 모든 태그 목록 보기

46. **그래프 이벤트 추가** (`add_graph_event`)
    - 그래프에 특정 이벤트 표시
    - 매개변수: `dashboard_id`, `panel_id`, `time`, `description`
    - 예시: 시스템 재시작 이벤트 표시

## 데이터 소스 관리

### 데이터 소스 일반 관리

47. **데이터 소스 목록 가져오기** (`list_datasources`)
    - 모든 구성된 데이터 소스 조회
    - 매개변수: `none`
    - 예시: 시스템에 연결된 모든 데이터 소스 나열

48. **데이터 소스 가져오기(UID)** (`get_datasource_by_uid`)
    - UID로 데이터 소스 조회
    - 매개변수: `uid`
    - 예시: 특정 UID로 프로메테우스 데이터 소스 상세 정보 확인

49. **데이터 소스 가져오기(이름)** (`get_datasource_by_name`)
    - 이름으로 데이터 소스 조회
    - 매개변수: `name`
    - 예시: "Production Prometheus"라는 데이터 소스 조회

50. **데이터 소스 가져오기(ID)** (`get_datasource_by_id`)
    - ID로 데이터 소스 조회
    - 매개변수: `id`
    - 예시: ID 42의 데이터 소스 상세 정보 확인

51. **데이터 소스 생성** (`create_datasource`)
    - 새 데이터 소스 추가
    - 매개변수: `name`, `type`, `url`, `access`, `basic_auth`, `json_data`
    - 예시: 새 프로메테우스 데이터 소스 연결 구성

52. **데이터 소스 업데이트** (`update_datasource`)
    - 기존 데이터 소스 수정
    - 매개변수: `id`, `name`, `type`, `url`, `access`, `basic_auth`, `json_data`
    - 예시: 데이터 소스 URL 및 인증 설정 변경

53. **데이터 소스 삭제** (`delete_datasource`)
    - 데이터 소스 제거
    - 매개변수: `id`
    - 예시: 사용하지 않는 데이터 소스 삭제

54. **데이터 소스 헬스 체크** (`check_datasource_health`)
    - 데이터 소스 연결 상태 확인
    - 매개변수: `id`
    - 예시: 데이터 소스 연결 가능 여부 테스트

55. **데이터 소스 프록시 테스트** (`test_datasource_proxy`)
    - 데이터 소스 프록시 기능 테스트
    - 매개변수: `id`, `path`
    - 예시: 프록시를 통한 API 엔드포인트 테스트

56. **데이터 소스 설정 가져오기** (`get_datasource_settings`)
    - 데이터 소스 플러그인 설정 옵션 조회
    - 매개변수: `type`
    - 예시: Elasticsearch 데이터 소스 설정 옵션 조회

57. **데이터 소스 권한 설정** (`update_datasource_permissions`)
    - 데이터 소스에 대한 접근 권한 설정
    - 매개변수: `id`, `permissions`
    - 예시: 특정 팀에 데이터 소스 쿼리 권한 부여

58. **데이터 소스 비밀정보 업데이트** (`update_datasource_secrets`)
    - 데이터 소스 비밀 키 정보 업데이트
    - 매개변수: `id`, `secrets`
    - 예시: 데이터 소스 API 키 갱신

### Prometheus 데이터 소스

59. **Prometheus 쿼리** (`query_prometheus`)
    - Prometheus 데이터 소스에 PromQL 쿼리 실행
    - 매개변수: `datasource_uid`, `expr`, `start_rfc3339`, `end_rfc3339`, `step_seconds`, `query_type`
    - 예시: 지난 6시간 동안의 CPU 사용률 조회

60. **Prometheus 메트릭 메타데이터 조회** (`list_prometheus_metric_metadata`)
    - 사용 가능한 메트릭에 대한 메타데이터 조회
    - 매개변수: `datasource_uid`, `limit`, `metric`
    - 예시: HTTP 요청 메트릭에 대한 도움말 및 타입 정보 조회

61. **Prometheus 메트릭 이름 조회** (`list_prometheus_metric_names`)
    - 사용 가능한 모든 메트릭 이름 나열
    - 매개변수: `datasource_uid`, `regex`, `limit`
    - 예시: 노드 관련 모든 메트릭 이름 찾기

62. **Prometheus 레이블 이름 조회** (`list_prometheus_label_names`)
    - 메트릭 선택기에 맞는 레이블 이름 조회
    - 매개변수: `datasource_uid`, `matches`, `start_rfc3339`, `end_rfc3339`
    - 예시: 특정 애플리케이션 메트릭에서 사용 가능한 모든 레이블 조회

63. **Prometheus 레이블 값 조회** (`list_prometheus_label_values`)
    - 특정 레이블에 대한 모든 값 조회
    - 매개변수: `datasource_uid`, `label_name`, `matches`, `start_rfc3339`, `end_rfc3339`
    - 예시: 환경 레이블에 대한 모든 가능한 값(prod, dev, staging 등) 조회

64. **Prometheus 시리즈 조회** (`query_prometheus_series`)
    - 메트릭 선택기에 맞는 시계열 조회
    - 매개변수: `datasource_uid`, `match[]`, `start`, `end`
    - 예시: 지난 1시간 동안 활성화된 모든 HTTP 요청 시리즈 조회

65. **Prometheus 인스턴트 쿼리** (`query_prometheus_instant`)
    - 특정 시점의 값에 대한 인스턴트 쿼리 실행
    - 매개변수: `datasource_uid`, `expr`, `time`
    - 예시: 현재 시점의 메모리 사용량 조회

66. **Prometheus 템플릿 변수 쿼리** (`query_prometheus_template_variable`)
    - 대시보드 템플릿 변수 채우기 위한 쿼리 실행
    - 매개변수: `datasource_uid`, `expr`
    - 예시: 사용 가능한 모든 Kubernetes 네임스페이스 조회

### Loki 데이터 소스

67. **Loki 로그 쿼리** (`query_loki_logs`)
    - Loki 데이터 소스에 LogQL 쿼리 실행하여 로그 검색
    - 매개변수: `datasource_uid`, `logql`, `start_rfc3339`, `end_rfc3339`, `limit`, `direction`
    - 예시: 특정 오류 메시지가 포함된 로그 검색

68. **Loki 레이블 이름 조회** (`list_loki_label_names`)
    - 사용 가능한 모든 로그 레이블 이름 조회
    - 매개변수: `datasource_uid`, `start_rfc3339`, `end_rfc3339`
    - 예시: 로그 데이터에서 사용 가능한 모든 키 조회

69. **Loki 레이블 값 조회** (`list_loki_label_values`)
    - 특정 레이블에 대한 모든 값 조회
    - 매개변수: `datasource_uid`, `label_name`, `start_rfc3339`, `end_rfc3339`
    - 예시: 서비스 레이블에 대한 모든 값 조회

70. **Loki 통계 조회** (`query_loki_stats`)
    - 로그 스트림에 대한 통계 조회
    - 매개변수: `datasource_uid`, `logql`, `start_rfc3339`, `end_rfc3339`
    - 예시: 로그 볼륨, 스트림 수, 데이터 크기 조회

71. **Loki 메트릭 쿼리** (`query_loki_metrics`)
    - LogQL 메트릭 쿼리 실행
    - 매개변수: `datasource_uid`, `logql`, `start_rfc3339`, `end_rfc3339`, `step`
    - 예시: 시간별 오류 빈도 메트릭 계산

72. **Loki 테일 쿼리** (`tail_loki_logs`)
    - 실시간 로그 스트리밍 (tail -f와 유사)
    - 매개변수: `datasource_uid`, `logql`, `limit`
    - 예시: 프로덕션 API 서비스의 실시간 로그 모니터링

73. **Loki 로그 파싱** (`parse_loki_logs`)
    - 정규식 또는 JSON으로 로그 구조화
    - 매개변수: `datasource_uid`, `logql`, `parse_expression`
    - 예시: JSON 로그에서 특정 필드 추출 및 필터링

74. **Loki 로그 볼륨 분석** (`analyze_loki_log_volume`)
    - 시간별 로그 볼륨 추세 분석
    - 매개변수: `datasource_uid`, `logql`, `interval`, `start_rfc3339`, `end_rfc3339`
    - 예시: 지난 24시간 동안 시간별 오류 로그 수 추세 분석 