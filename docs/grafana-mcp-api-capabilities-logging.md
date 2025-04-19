# Grafana MCP API 기능 목록: 로깅 및 모니터링

이 문서는 MCP(Model Context Protocol)를 통해 Grafana에서 제공할 수 있는 로깅 및 모니터링 관련 기능들을 상세히 정리한 것입니다.

## 로깅 및 모니터링

### 로그 쿼리 및 분석

119. **로그 쿼리** (`query_logs`)
    - 다양한 로그 데이터 소스(Loki, Elasticsearch 등)에서 로그 검색
    - 매개변수: `datasource_uid`, `query`, `time_range`, `limit`
    - 예시: 여러 데이터 소스에서 오류 로그 통합 검색

120. **로그 패턴 분석** (`analyze_log_patterns`)
    - 로그에서 반복적인 패턴 자동 식별
    - 매개변수: `datasource_uid`, `query`, `time_range`
    - 예시: 비정상적인 로그 패턴 자동 감지

121. **로그 통계 분석** (`analyze_log_statistics`)
    - 로그 메시지 빈도, 분포, 추세 분석
    - 매개변수: `datasource_uid`, `query`, `time_range`, `group_by`
    - 예시: 상위 오류 메시지 유형 및 빈도 분석

122. **로그 히스토그램 생성** (`create_log_histogram`)
    - 시간별 로그 볼륨 히스토그램 생성
    - 매개변수: `datasource_uid`, `query`, `time_range`, `interval`
    - 예시: 10분 간격으로 오류 로그 분포 시각화

123. **로그 라인 상세 조회** (`get_log_line_details`)
    - 특정 로그 라인의 전체 메타데이터 및 컨텍스트 조회
    - 매개변수: `datasource_uid`, `log_id`, `context_size`
    - 예시: 오류 로그 이전/이후 로그 라인 확인

124. **로그 필터 생성** (`create_log_filter`)
    - 로그 뷰에 필터 적용
    - 매개변수: `datasource_uid`, `filters`
    - 예시: 특정 서비스 및 오류 수준 로그만 표시

125. **로그 컨텍스트 조회** (`get_log_context`)
    - 특정 로그 주변의 컨텍스트 로그 조회
    - 매개변수: `datasource_uid`, `log_id`, `direction`, `limit`
    - 예시: 오류 로그 이전 20개 로그 메시지 확인

126. **구조화된 로그 필드 추출** (`extract_log_fields`)
    - 로그 메시지에서 구조화된 필드 추출
    - 매개변수: `datasource_uid`, `log_line`, `extraction_rules`
    - 예시: JSON 로그에서 특정 필드 추출

127. **로그 쿼리 작성 지원** (`get_log_query_suggestions`)
    - 로그 쿼리 자동 완성 및 제안
    - 매개변수: `datasource_uid`, `query_prefix`
    - 예시: Loki 쿼리 구문 자동 완성 제안

### 메트릭 모니터링

128. **메트릭 쿼리** (`query_metrics`)
    - 다양한 데이터 소스에서 메트릭 쿼리 실행
    - 매개변수: `datasource_uid`, `query`, `time_range`, `interval`
    - 예시: 여러 데이터 소스에서 CPU 사용률 조회

129. **메트릭 비교** (`compare_metrics`)
    - 서로 다른 시간대의 메트릭 비교
    - 매개변수: `datasource_uid`, `query`, `time_range_a`, `time_range_b`
    - 예시: 이번 주와 지난 주의 API 응답 시간 비교

130. **메트릭 계산** (`calculate_metric`)
    - 기존 메트릭을 기반으로 새 메트릭 계산
    - 매개변수: `datasource_uid`, `expression`, `time_range`
    - 예시: 요청 수와 오류 수로 오류율 계산

131. **메트릭 이상 감지** (`detect_metric_anomalies`)
    - 메트릭에서 비정상적인 패턴 감지
    - 매개변수: `datasource_uid`, `query`, `time_range`, `algorithm`
    - 예시: CPU 사용량의 비정상적인 급증 감지

132. **메트릭 경향 분석** (`analyze_metric_trends`)
    - 메트릭 추세 및 패턴 분석
    - 매개변수: `datasource_uid`, `query`, `time_range`
    - 예시: 메모리 사용량 증가 추세 분석

133. **메트릭 예측** (`predict_metric_values`)
    - 과거 데이터 기반 미래 메트릭 값 예측
    - 매개변수: `datasource_uid`, `query`, `prediction_range`, `algorithm`
    - 예시: 다음 24시간 동안의 디스크 사용량 예측

134. **메트릭 히스토그램 생성** (`create_metric_histogram`)
    - 메트릭 값 분포 히스토그램 생성
    - 매개변수: `datasource_uid`, `query`, `time_range`, `buckets`
    - 예시: API 응답 시간 분포 시각화

135. **메트릭 히트맵 생성** (`create_metric_heatmap`)
    - 시간 및 값 기반 메트릭 히트맵 생성
    - 매개변수: `datasource_uid`, `query`, `time_range`, `y_buckets`
    - 예시: 시간별 HTTP 상태 코드 분포 히트맵

136. **메트릭 상관관계 분석** (`analyze_metric_correlations`)
    - 여러 메트릭 간의 상관관계 분석
    - 매개변수: `datasource_uid`, `metrics`, `time_range`
    - 예시: CPU 사용량과 응답 시간 간의 상관관계 분석

### 로그-메트릭 통합 분석

137. **로그-메트릭 상관관계 분석** (`correlate_logs_and_metrics`)
    - 로그 이벤트와 메트릭 변화 간의 상관관계 분석
    - 매개변수: `log_datasource_uid`, `log_query`, `metric_datasource_uid`, `metric_query`, `time_range`
    - 예시: 오류 로그 발생과 서비스 지연 간의 관계 분석

138. **메트릭에서 로그로 드릴다운** (`drilldown_from_metric_to_logs`)
    - 메트릭 데이터 포인트에서 관련 로그 조회
    - 매개변수: `metric_datasource_uid`, `metric_query`, `timestamp`, `log_datasource_uid`
    - 예시: CPU 스파이크 시점의 관련 시스템 로그 조회

139. **로그 기반 메트릭 생성** (`create_metrics_from_logs`)
    - 로그 쿼리 결과를 기반으로 메트릭 생성
    - 매개변수: `log_datasource_uid`, `log_query`, `metric_name`, `aggregation`
    - 예시: 오류 로그 빈도를 메트릭으로 변환

### 상태 모니터링

140. **시스템 상태 조회** (`get_system_health`)
    - 모니터링 대상 시스템의 전반적인 상태 조회
    - 매개변수: `dashboard_uid`
    - 예시: 모든 프로덕션 서비스의 종합 상태 확인

141. **컴포넌트 상태 조회** (`get_component_health`)
    - 특정 시스템 컴포넌트의 상태 조회
    - 매개변수: `component_id`
    - 예시: 데이터베이스 클러스터 상태 확인

142. **서비스 가용성 조회** (`get_service_availability`)
    - 서비스 가용성 메트릭 및 SLA 계산
    - 매개변수: `service_id`, `time_range`
    - 예시: 지난 30일 동안의 API 가용성 비율 계산

143. **상태 변경 이력 조회** (`get_health_status_history`)
    - 시스템 상태 변경 이력 조회
    - 매개변수: `component_id`, `time_range`
    - 예시: 서비스가 언제 다운되었는지 이력 조회

144. **지연 시간 분석** (`analyze_latency`)
    - 서비스 응답 시간 분석
    - 매개변수: `service_id`, `time_range`, `percentiles`
    - 예시: API 응답 시간의 p95, p99 계산

145. **오류율 분석** (`analyze_error_rates`)
    - 서비스 오류율 계산 및 분석
    - 매개변수: `service_id`, `time_range`, `group_by`
    - 예시: API 엔드포인트별 오류율 계산

146. **리소스 포화도 분석** (`analyze_resource_saturation`)
    - 시스템 리소스 사용량 및 포화도 분석
    - 매개변수: `resource_type`, `component_id`, `time_range`
    - 예시: 메모리, CPU, 디스크, 네트워크 포화도 확인

147. **트래픽 분석** (`analyze_traffic`)
    - 시스템 트래픽 패턴 및 볼륨 분석
    - 매개변수: `service_id`, `time_range`, `group_by`
    - 예시: 시간별, 요일별 API 요청 볼륨 분석

### 이벤트 모니터링

148. **이벤트 조회** (`get_events`)
    - 모니터링 시스템에서 캡처한 이벤트 조회
    - 매개변수: `time_range`, `tags`, `limit`
    - 예시: 지난 24시간 동안의 모든 배포 이벤트 조회

149. **이벤트 생성** (`create_event`)
    - 시스템에 새 이벤트 기록
    - 매개변수: `title`, `text`, `tags`, `timestamp`
    - 예시: 배포 완료 이벤트 기록

150. **이벤트 주석 추가** (`annotate_event`)
    - 기존 이벤트에 추가 정보 주석 추가
    - 매개변수: `event_id`, `text`, `created_by`
    - 예시: 이벤트에 해결 방법 정보 추가

151. **이벤트 상관관계 분석** (`correlate_events`)
    - 여러 이벤트 간의 상관관계 분석
    - 매개변수: `event_ids`, `time_window`
    - 예시: 배포 이벤트와 오류 증가 간의 상관관계 분석

152. **이벤트 타임라인 생성** (`create_event_timeline`)
    - 여러 이벤트를 포함한 타임라인 생성
    - 매개변수: `events`, `time_range`
    - 예시: 시스템 장애 기간 동안의 모든 이벤트 시각화

153. **이벤트 태그 관리** (`manage_event_tags`)
    - 이벤트 태그 추가, 제거 또는 수정
    - 매개변수: `event_id`, `tags_to_add`, `tags_to_remove`
    - 예시: 이벤트에 "해결됨" 태그 추가

### 시스템 메트릭 모니터링

154. **호스트 메트릭 조회** (`get_host_metrics`)
    - 호스트 레벨 시스템 메트릭 조회
    - 매개변수: `host_id`, `metrics`, `time_range`
    - 예시: 특정 서버의 CPU, 메모리, 디스크, 네트워크 지표 조회

155. **컨테이너 메트릭 조회** (`get_container_metrics`)
    - 컨테이너 레벨 시스템 메트릭 조회
    - 매개변수: `container_id`, `metrics`, `time_range`
    - 예시: 특정 Docker 컨테이너의 리소스 사용량 조회

156. **애플리케이션 메트릭 조회** (`get_application_metrics`)
    - 애플리케이션 레벨 성능 메트릭 조회
    - 매개변수: `application_id`, `metrics`, `time_range`
    - 예시: 웹 애플리케이션의 응답 시간, 처리량, 오류율 조회

157. **데이터베이스 메트릭 조회** (`get_database_metrics`)
    - 데이터베이스 성능 메트릭 조회
    - 매개변수: `database_id`, `metrics`, `time_range`
    - 예시: PostgreSQL 인스턴스의 쿼리 실행 시간, 연결 수, 캐시 적중률 조회

158. **네트워크 메트릭 조회** (`get_network_metrics`)
    - 네트워크 성능 및 트래픽 메트릭 조회
    - 매개변수: `network_id`, `metrics`, `time_range`
    - 예시: 네트워크 인터페이스의 대역폭 사용량, 패킷 손실, 지연 시간 조회

159. **클라우드 서비스 메트릭 조회** (`get_cloud_service_metrics`)
    - 클라우드 제공업체의 서비스 메트릭 조회
    - 매개변수: `provider`, `service_type`, `service_id`, `metrics`, `time_range`
    - 예시: AWS RDS 인스턴스의 성능 메트릭 조회

160. **Kubernetes 메트릭 조회** (`get_kubernetes_metrics`)
    - Kubernetes 클러스터 및 워크로드 메트릭 조회
    - 매개변수: `cluster_id`, `namespace`, `workload_type`, `workload_name`, `metrics`, `time_range`
    - 예시: Kubernetes 배포의 Pod CPU 및 메모리 사용량 조회 