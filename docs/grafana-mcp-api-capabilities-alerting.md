# Grafana MCP API 기능 목록: 알림 및 알림 관리

이 문서는 MCP(Model Context Protocol)를 통해 Grafana에서 제공할 수 있는 알림 및 알림 관리 관련 기능들을 상세히 정리한 것입니다.

## 알림 및 알림 관리

### 알림 규칙 관리

75. **알림 규칙 목록 조회** (`list_alert_rules`)
    - 구성된 모든 알림 규칙 조회
    - 매개변수: `folder_uid`, `dashboard_id`
    - 예시: 특정 폴더 또는 대시보드의 모든 알림 규칙 조회

76. **알림 규칙 상세 조회** (`get_alert_rule_by_uid`)
    - UID로 특정 알림 규칙 상세 정보 조회
    - 매개변수: `uid`
    - 예시: 특정 알림 규칙의 조건, 알림 설정, 상태 조회

77. **알림 규칙 생성** (`create_alert_rule`)
    - 새 알림 규칙 생성
    - 매개변수: `title`, `condition`, `data`, `no_data_state`, `exec_err_state`, `for`, `folder_uid`, `annotations`, `labels`
    - 예시: CPU 사용량 90% 초과 시 알림 발생하는 규칙 생성

78. **알림 규칙 업데이트** (`update_alert_rule`)
    - 기존 알림 규칙 수정
    - 매개변수: `uid`, `title`, `condition`, `data`, `no_data_state`, `exec_err_state`, `for`, `annotations`, `labels`
    - 예시: 알림 임계값 조정 및 라벨 업데이트

79. **알림 규칙 삭제** (`delete_alert_rule`)
    - 알림 규칙 삭제
    - 매개변수: `uid`
    - 예시: 더 이상 필요하지 않은 알림 규칙 제거

80. **알림 규칙 일시중지** (`pause_alert_rule`)
    - 알림 규칙 실행 일시중지
    - 매개변수: `uid`
    - 예시: 유지보수 작업 중 알림 발생 방지

81. **알림 규칙 재개** (`unpause_alert_rule`)
    - 일시중지된 알림 규칙 재개
    - 매개변수: `uid`
    - 예시: 유지보수 완료 후 알림 모니터링 재개

82. **알림 규칙 그룹화** (`group_alert_rules`)
    - 유사한 알림 규칙 그룹으로 조직화
    - 매개변수: `folder_uid`, `group_name`, `rule_uids`
    - 예시: 관련 서비스별로 알림 규칙 그룹화

83. **알림 규칙 테스트** (`test_alert_rule`)
    - 알림 규칙 조건 테스트
    - 매개변수: `condition`, `data`
    - 예시: 실제 알림 발송 없이 알림 규칙 로직 테스트

84. **알림 규칙 상태 조회** (`get_alert_rule_state`)
    - 알림 규칙의 현재 상태 조회
    - 매개변수: `uid`
    - 예시: 알림 규칙이 정상, 경고, 알림 상태인지 확인

85. **알림 규칙 이력 조회** (`get_alert_rule_history`)
    - 알림 규칙 상태 변경 이력 조회
    - 매개변수: `uid`, `limit`
    - 예시: 알림 규칙의 지난 10회 상태 변경 조회

### 알림 인스턴스 관리

86. **알림 인스턴스 목록 조회** (`list_alert_instances`)
    - 현재 활성화된 모든 알림 인스턴스 조회
    - 매개변수: `rule_uid`, `state`
    - 예시: 현재 발생(firing) 상태인 모든 알림 조회

87. **알림 인스턴스 상세 조회** (`get_alert_instance`)
    - 특정 알림 인스턴스의 상세 정보 조회
    - 매개변수: `rule_uid`, `labels_hash`
    - 예시: 발생한 알림의 라벨, 값, 상태 상세 정보 확인

88. **알림 인스턴스 목록 필터링** (`filter_alert_instances`)
    - 라벨 또는 상태별 알림 인스턴스 필터링
    - 매개변수: `labels`, `state`
    - 예시: 특정 서비스 및 환경에 관련된 알림만 조회

89. **알림 인스턴스 일시중지** (`silence_alert_instance`)
    - 특정 알림 인스턴스 일시중지 (사일런스 생성)
    - 매개변수: `matchers`, `starts_at`, `ends_at`, `comment`, `created_by`
    - 예시: 알려진 문제에 대한 알림을 2시간 동안 일시중지

### 알림 통지 채널 관리

90. **연락처 목록 조회** (`list_contact_points`)
    - 구성된 모든 알림 연락처 조회
    - 매개변수: `none`
    - 예시: 이메일, Slack, PagerDuty 등 모든 연락처 채널 조회

91. **연락처 상세 조회** (`get_contact_point`)
    - 특정 연락처의 상세 정보 조회
    - 매개변수: `uid`
    - 예시: Slack 연락처 채널의 웹훅 URL 및 설정 확인

92. **연락처 생성** (`create_contact_point`)
    - 새 알림 연락처 생성
    - 매개변수: `name`, `type`, `settings`
    - 예시: 새 Slack 채널로 알림을 보내는 연락처 생성

93. **연락처 업데이트** (`update_contact_point`)
    - 기존 연락처 설정 수정
    - 매개변수: `uid`, `name`, `type`, `settings`
    - 예시: 이메일 수신자 목록 업데이트

94. **연락처 삭제** (`delete_contact_point`)
    - 연락처 삭제
    - 매개변수: `uid`
    - 예시: 더 이상 사용하지 않는 WebEx 연락처 제거

95. **연락처 테스트** (`test_contact_point`)
    - 연락처로 테스트 알림 전송
    - 매개변수: `uid`, `message`
    - 예시: 새로 구성한 이메일 연락처가 제대로 작동하는지 테스트

### 알림 정책 관리

96. **알림 정책 조회** (`get_notification_policies`)
    - 알림 라우팅 정책 트리 조회
    - 매개변수: `none`
    - 예시: 모든 알림 라우팅 정책 계층 구조 확인

97. **알림 정책 업데이트** (`update_notification_policies`)
    - 알림 라우팅 정책 트리 업데이트
    - 매개변수: `policy_tree`
    - 예시: 새로운 알림 라우팅 정책 구성 적용

98. **알림 정책 테스트** (`test_notification_routing`)
    - 라벨 집합에 대한 알림 라우팅 테스트
    - 매개변수: `labels`
    - 예시: 특정 라벨이 있는 알림이 어떤 연락처로 라우팅되는지 테스트

### 사일런스 관리

99. **사일런스 목록 조회** (`list_silences`)
    - 현재 활성화된 모든 사일런스 조회
    - 매개변수: `filter`
    - 예시: 만료되지 않은 모든 사일런스 조회

100. **사일런스 생성** (`create_silence`)
     - 새 사일런스 생성하여 특정 알림 일시중지
     - 매개변수: `matchers`, `starts_at`, `ends_at`, `comment`, `created_by`
     - 예시: 계획된 유지보수 동안 특정 서버 알림 일시중지

101. **사일런스 상세 조회** (`get_silence`)
     - 특정 사일런스 상세 정보 조회
     - 매개변수: `id`
     - 예시: 사일런스의 적용 범위, 기간, 생성자 확인

102. **사일런스 업데이트** (`update_silence`)
     - 기존 사일런스 수정
     - 매개변수: `id`, `matchers`, `starts_at`, `ends_at`, `comment`
     - 예시: 사일런스 기간 연장

103. **사일런스 삭제** (`delete_silence`)
     - 사일런스 삭제하여 알림 재활성화
     - 매개변수: `id`
     - 예시: 예정보다 일찍 유지보수가 완료되어 사일런스 제거

### 알림 템플릿 관리

104. **알림 템플릿 목록 조회** (`list_alert_templates`)
     - 구성된 모든 알림 템플릿 조회
     - 매개변수: `none`
     - 예시: 사용 가능한, 변수가 있는 모든 알림 템플릿 조회

105. **알림 템플릿 생성** (`create_alert_template`)
     - 새 알림 템플릿 생성
     - 매개변수: `name`, `template`
     - 예시: 새로운 서비스 중단 알림 형식 템플릿 생성

106. **알림 템플릿 상세 조회** (`get_alert_template`)
     - 특정 알림 템플릿 상세 정보 조회
     - 매개변수: `name`
     - 예시: 기존 템플릿의 내용 및 변수 확인

107. **알림 템플릿 업데이트** (`update_alert_template`)
     - 기존 알림 템플릿 수정
     - 매개변수: `name`, `template`
     - 예시: 기존 템플릿에 새 메타데이터 필드 추가

108. **알림 템플릿 삭제** (`delete_alert_template`)
     - 알림 템플릿 삭제
     - 매개변수: `name`
     - 예시: 더 이상 사용하지 않는 템플릿 제거

109. **알림 템플릿 테스트** (`test_alert_template`)
     - 템플릿 렌더링 테스트
     - 매개변수: `template`, `data`
     - 예시: 샘플 알림 데이터로 템플릿 출력 미리보기

### 알림 이벤트 관리

110. **알림 이벤트 조회** (`list_alert_events`)
     - 알림 규칙의 이벤트 이력 조회
     - 매개변수: `rule_uid`, `limit`
     - 예시: 특정 알림 규칙이 언제 활성화/비활성화되었는지 이력 확인

111. **알림 요약 조회** (`get_alert_summary`)
     - 현재 알림 상태의 통계 요약 조회
     - 매개변수: `include_instance_count`
     - 예시: 상태별(정상, 보류 중, 발생) 알림 규칙 수 확인

112. **알림 이벤트 필터링** (`filter_alert_events`)
     - 특정 조건으로 알림 이벤트 필터링
     - 매개변수: `from`, `to`, `rule_uid`, `state`
     - 예시: 지난 24시간 동안 발생한 모든 실패 알림 이벤트 조회

### 알림 구성 프로비저닝

113. **알림 구성 내보내기** (`export_alerting_config`)
     - 알림 규칙, 연락처, 정책을 파일로 내보내기
     - 매개변수: `format`
     - 예시: 현재 알림 구성을 YAML 파일로 내보내 저장

114. **알림 구성 가져오기** (`import_alerting_config`)
     - 파일에서 알림 구성 가져오기
     - 매개변수: `config`, `overwrite`
     - 예시: 다른 환경의 알림 구성을 현재 환경으로 복제

115. **알림 구성 검증** (`validate_alerting_config`)
     - 알림 구성 파일의 유효성 검사
     - 매개변수: `config`
     - 예시: 알림 구성 파일이 문법적으로 유효한지 확인

116. **알림 구성 백업** (`backup_alerting_config`)
     - 현재 알림 구성의 스냅샷 생성
     - 매개변수: `none`
     - 예시: 주요 변경 전 현재 구성 백업

### 알림 수신 관리

117. **알림 스크래핑 상태 조회** (`get_alertmanager_receiver_status`)
     - AlertManager의 수신자 상태 확인
     - 매개변수: `none`
     - 예시: 모든 알림 수신자 가용성 상태 확인

118. **알림 외부 연동 상태 조회** (`get_alertmanager_integration_status`)
     - 외부 알림 시스템 연동 상태 조회
     - 매개변수: `integration_type`
     - 예시: PagerDuty 연동 상태 확인 