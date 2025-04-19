# Grafana MCP API 기능 목록: 트레이싱 및 프로파일링

이 문서는 MCP(Model Context Protocol)를 통해 Grafana에서 제공할 수 있는 트레이싱 및 프로파일링 관련 기능들을 상세히 정리한 것입니다.

## 트레이싱 및 프로파일링

### 분산 트레이싱 (Tempo)

161. **트레이스 쿼리** (`query_traces`)
    - 트레이스 데이터 소스에서 트레이스 검색
    - 매개변수: `datasource_uid`, `query_type`, `query`, `limit`
    - 예시: 특정 서비스 또는 태그가 있는 트레이스 검색

162. **트레이스 ID로 조회** (`get_trace_by_id`)
    - 트레이스 ID로 전체 트레이스 상세 정보 조회
    - 매개변수: `datasource_uid`, `trace_id`
    - 예시: 특정 트레이스 ID에 대한 모든 스팬 정보 조회

163. **서비스 그래프 생성** (`create_service_graph`)
    - 트레이스 데이터 기반 서비스 종속성 그래프 생성
    - 매개변수: `datasource_uid`, `time_range`
    - 예시: 마이크로서비스 간 통신 패턴 및 의존성 시각화

164. **트레이스 비교** (`compare_traces`)
    - 두 트레이스의 차이점 분석
    - 매개변수: `datasource_uid`, `trace_id_a`, `trace_id_b`
    - 예시: 성공한 요청과 실패한 요청의 트레이스 비교

165. **트레이스 통계 조회** (`get_trace_statistics`)
    - 트레이스 메트릭 및 통계 조회
    - 매개변수: `datasource_uid`, `service_name`, `span_name`, `time_range`
    - 예시: 특정 서비스의 평균 지연 시간, 오류율 등 조회

166. **트레이스 히스토그램 생성** (`create_trace_histogram`)
    - 트레이스 기간 분포 히스토그램 생성
    - 매개변수: `datasource_uid`, `service_name`, `span_name`, `time_range`
    - 예시: 특정 API 엔드포인트의 지연 시간 분포 시각화

167. **스팬 필터링** (`filter_spans`)
    - 특정 조건에 맞는 스팬 필터링
    - 매개변수: `datasource_uid`, `trace_id`, `filters`
    - 예시: 특정 트레이스 내에서 500ms 이상 걸린 스팬만 조회

168. **스팬 상세 정보 조회** (`get_span_details`)
    - 특정 스팬의 상세 정보, 태그, 로그 조회
    - 매개변수: `datasource_uid`, `trace_id`, `span_id`
    - 예시: 오류가 발생한 스팬의 상세 정보 및 로그 확인

169. **서비스별 트레이스 분석** (`analyze_traces_by_service`)
    - 특정 서비스의 트레이스 패턴 분석
    - 매개변수: `datasource_uid`, `service_name`, `time_range`
    - 예시: 데이터베이스 서비스의 트레이스 성능 패턴 분석

170. **엔드포인트별 트레이스 분석** (`analyze_traces_by_endpoint`)
    - 특정 엔드포인트의 트레이스 패턴 분석
    - 매개변수: `datasource_uid`, `service_name`, `endpoint`, `time_range`
    - 예시: 사용자 로그인 API의 트레이스 성능 분석

171. **트레이스-로그 통합 조회** (`get_logs_for_trace`)
    - 특정 트레이스와 관련된 로그 조회
    - 매개변수: `trace_datasource_uid`, `trace_id`, `log_datasource_uid`
    - 예시: 트레이스 ID를 기반으로 관련 로그 메시지 검색

172. **트레이스-메트릭 통합 조회** (`get_metrics_for_trace`)
    - 특정 트레이스 기간 동안의 관련 메트릭 조회
    - 매개변수: `trace_datasource_uid`, `trace_id`, `metric_datasource_uid`, `metrics`
    - 예시: 트레이스가 실행된 시간 동안의 시스템 리소스 사용량 조회

173. **이상 트레이스 감지** (`detect_anomalous_traces`)
    - 비정상적인 성능 특성을 보이는 트레이스 자동 감지
    - 매개변수: `datasource_uid`, `service_name`, `time_range`, `detection_method`
    - 예시: 평균보다 10배 느린 트레이스 자동 감지

174. **트레이스 경로 분석** (`analyze_trace_paths`)
    - 요청이 시스템을 통과하는 경로 분석
    - 매개변수: `datasource_uid`, `service_name`, `operation_name`, `time_range`
    - 예시: 사용자 요청이 마이크로서비스를 통과하는 모든 가능한 경로 식별

175. **병목 현상 감지** (`detect_trace_bottlenecks`)
    - 트레이스에서 성능 병목 구간 자동 감지
    - 매개변수: `datasource_uid`, `trace_id`
    - 예시: 전체 응답 시간의 50% 이상을 차지하는 스팬 식별

176. **태그 기반 트레이스 검색** (`search_traces_by_tags`)
    - 태그 기반으로 트레이스 검색
    - 매개변수: `datasource_uid`, `tags`, `time_range`
    - 예시: 특정 사용자 ID가 포함된 모든 트레이스 검색

### 연속 프로파일링 (Pyroscope)

177. **프로파일 쿼리** (`query_profiles`)
    - 프로파일링 데이터 소스에서 프로파일 쿼리
    - 매개변수: `datasource_uid`, `query`, `time_range`, `profile_type`
    - 예시: 특정 애플리케이션의 CPU 프로파일 조회

178. **플레임 그래프 생성** (`create_flame_graph`)
    - 프로파일 데이터 기반 플레임 그래프 생성
    - 매개변수: `datasource_uid`, `query`, `time_range`, `profile_type`
    - 예시: 메모리 사용량에 대한 플레임 그래프 시각화

179. **테이블 뷰 생성** (`create_profile_table`)
    - 프로파일 데이터 기반 테이블 뷰 생성
    - 매개변수: `datasource_uid`, `query`, `time_range`, `profile_type`, `grouping`
    - 예시: 함수별로 그룹화된 CPU 시간 테이블 생성

180. **프로파일 비교** (`compare_profiles`)
    - 서로 다른 기간 또는 버전의 프로파일 비교
    - 매개변수: `datasource_uid`, `query_a`, `time_range_a`, `query_b`, `time_range_b`, `profile_type`
    - 예시: 배포 전후의 메모리 프로파일 비교

181. **상위 호출 스택 분석** (`analyze_top_stacks`)
    - 리소스 사용량이 가장 높은 호출 스택 분석
    - 매개변수: `datasource_uid`, `query`, `time_range`, `profile_type`, `limit`
    - 예시: CPU 시간을 가장 많이 소비하는 호출 스택 순위 조회

182. **함수별 리소스 사용량 분석** (`analyze_function_resource_usage`)
    - 개별 함수의 리소스 사용량 분석
    - 매개변수: `datasource_uid`, `query`, `time_range`, `profile_type`, `function_name`
    - 예시: 특정 함수의 CPU 사용량 추세 분석

183. **프로파일 시계열 추세 분석** (`analyze_profile_trends`)
    - 시간에 따른 프로파일 변화 분석
    - 매개변수: `datasource_uid`, `query`, `time_range`, `profile_type`, `aggregation`
    - 예시: 시간별 메모리 할당 패턴 분석

184. **프로파일 이상 감지** (`detect_profile_anomalies`)
    - 프로파일에서 비정상적인 패턴 감지
    - 매개변수: `datasource_uid`, `query`, `time_range`, `profile_type`, `baseline_range`
    - 예시: 이전 기간과 비교하여 급격한 CPU 사용량 변화 감지

185. **메모리 누수 분석** (`analyze_memory_leaks`)
    - 메모리 프로파일을 통한 메모리 누수 분석
    - 매개변수: `datasource_uid`, `query`, `time_range`
    - 예시: 시간이 지남에 따라 메모리 사용량이 증가하는 객체 식별

186. **대기 시간 분석** (`analyze_wait_times`)
    - 블로킹 프로파일을 통한 대기 시간 분석
    - 매개변수: `datasource_uid`, `query`, `time_range`
    - 예시: 락 획득 또는 I/O 작업을 위해 대기하는 시간 분석

187. **고루틴/스레드 프로파일 분석** (`analyze_concurrency_profiles`)
    - 동시성 프로파일을 통한 스레드/고루틴 작업 분석
    - 매개변수: `datasource_uid`, `query`, `time_range`
    - 예시: 고루틴 차단 또는 스레드 폭발 문제 분석

188. **애플리케이션별 프로파일 비교** (`compare_application_profiles`)
    - 여러 애플리케이션 또는 서비스의 프로파일 비교
    - 매개변수: `datasource_uid`, `queries`, `time_range`, `profile_type`
    - 예시: 마이크로서비스 간의 CPU 사용 패턴 비교

189. **프로파일 히트맵 생성** (`create_profile_heatmap`)
    - 시간별 프로파일 변화를 보여주는 히트맵 생성
    - 매개변수: `datasource_uid`, `query`, `time_range`, `profile_type`
    - 예시: 함수별 CPU 사용량 변화를 시간순으로 시각화

190. **프로파일 태그 필터링** (`filter_profiles_by_tags`)
    - 특정 태그가 있는 프로파일만 필터링
    - 매개변수: `datasource_uid`, `tags`, `time_range`, `profile_type`
    - 예시: 특정 환경 또는 버전 태그가 있는 프로파일만 분석

### 합성 모니터링

191. **합성 모니터 목록 조회** (`list_synthetic_monitors`)
    - 구성된 모든 합성 모니터 조회
    - 매개변수: `none`
    - 예시: 모든 활성 상태 체크 및 브라우저 테스트 조회

192. **합성 모니터 생성** (`create_synthetic_monitor`)
    - 새 합성 모니터 생성
    - 매개변수: `name`, `target`, `frequency`, `timeout`, `probe_locations`, `job_type`, `settings`
    - 예시: 5분마다 웹사이트 가용성을 체크하는 HTTP 모니터 생성

193. **합성 모니터 상세 조회** (`get_synthetic_monitor`)
    - 특정 모니터의 상세 정보 조회
    - 매개변수: `monitor_id`
    - 예시: API 엔드포인트 모니터의 구성 및 상태 확인

194. **합성 모니터 업데이트** (`update_synthetic_monitor`)
    - 기존 합성 모니터 수정
    - 매개변수: `monitor_id`, `name`, `target`, `frequency`, `timeout`, `probe_locations`, `settings`
    - 예시: 체크 주기 변경 및 새 지역 추가

195. **합성 모니터 삭제** (`delete_synthetic_monitor`)
    - 합성 모니터 삭제
    - 매개변수: `monitor_id`
    - 예시: 더 이상 필요 없는 모니터 제거

196. **합성 모니터 결과 조회** (`get_synthetic_monitor_results`)
    - 합성 모니터의 체크 결과 이력 조회
    - 매개변수: `monitor_id`, `time_range`, `limit`
    - 예시: 지난 24시간 동안의 모든 체크 결과 조회

197. **합성 체크 결과 상세 조회** (`get_synthetic_check_result`)
    - 특정 체크 실행에 대한 상세 결과 조회
    - 매개변수: `check_id`
    - 예시: 실패한 브라우저 테스트의 스크린샷, HAR 파일, 로그 조회

198. **합성 모니터 가용성 분석** (`analyze_synthetic_monitor_availability`)
    - 모니터의 가용성 및 성능 메트릭 분석
    - 매개변수: `monitor_id`, `time_range`
    - 예시: 지난 30일 동안의 가동 시간, 응답 시간 추세 분석

199. **합성 모니터 알림 구성** (`configure_synthetic_monitor_alerts`)
    - 합성 모니터에 대한 알림 설정
    - 매개변수: `monitor_id`, `alert_settings`
    - 예시: 연속 3회 실패 시 알림 발생하도록 구성

200. **합성 모니터 즉시 실행** (`run_synthetic_monitor_now`)
    - 예약된 시간을 기다리지 않고 즉시 모니터 실행
    - 매개변수: `monitor_id`
    - 예시: 변경 사항 적용 후 즉시 테스트 실행 