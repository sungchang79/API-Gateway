## Application Service > API Gateway > API 오류 코드

|오류 코드|오류 메시지|설명|
|---|---|---|
|0|SUCCESS|성공|
|-1|FAIL|실패|
|400100000|Invalid request.|잘못된 요청입니다.|
|400100001|Invalid value in the request.|요청에 잘못된 값이 있습니다.|
|400100002|Invalid header name.|잘못된 형식의 헤더 이름입니다.|
|401100000|Invalid appKey.|잘못된 앱키입니다.|
|401100001|Invalid uuid.|사용자 정보가 유효하지 않습니다.|
|403100000|Not allowed user.|권한이 없습니다.|
|409100000|Could not complete the request due to a duplicate request.|중복 요청으로 인해 요청을 완료할 수 없습니다.|
|500100000|DB query failed.|일시적인 오류입니다. 오류가 지속되면 고객 센터로 문의해주시기 바랍니다.|
|400101000|Exceeded the maximum service count.|서비스 최대 생성 개수를 초과하였습니다.|
|404101000|Could not find API Gateway service.|API Gateway 서비스가 존재하지 않습니다.|
|400102000|There are no resources to stage.|생성된 리소스의 메서드가 없어 스테이지를 생성할 수 없습니다.|
|400102005|Invalid x-nhncloud-apigateway plugins.|x-nhncloud-apigateway plugins 필드에 잘못된 값이 있습니다.|
|400102012|Exceeded the maximum resource method count.|리소스 메서드의 최대 생성 개수를 초과하였습니다.|
|400102013|There are no resources to create.|생성할 리소스가 없습니다.|
|400102014|Failed to delete root resource.|루트('/') 리소스는 삭제할 수 없습니다.|
|400102015|Invalid resource plugin configuration.|리소스 플러그인 설정이 잘못되었습니다.|
|409102000|Failed to create duplicated resources.|중복된 경로 리소스는 생성할 수 없습니다.|
|400103000|Path variable cannot be used. Only variables declared for the selected path or above can be set.|잘못된 경로 변수입니다.|
|400103001|Failed to update stage resource. Stage resource plugin's position is invalid.|요청한 리소스에 설정할 수 없는 스테이지 플러그인입니다.|
|400103002|Failed to update stage resource. PRE_API's URL is not allowed to use stage URL.|잘못된 사전 호출의 URL 형식입니다.|
|400103003|Failed to update stage resource. Custom endpoint URL is not allowed at this stage resource path.|백엔드 엔드포인트 URL 재정의를 설정할 수 없는 리소스입니다.|
|400103004|Failed to create or update stage. Invalid backend endpoint URL format.|잘못된 백엔드 엔드포인트 URL 형식입니다.|
|400103005|Failed to delete stage. The stage have connected usage plan.|스테이지가 연결된 사용량 계획이 있습니다. 스테이지 연결 해제 후 스테이지를 삭제할 수 있습니다.|
|400103006|Exceeded the maximum stage count.|스테이지 최대 생성 개수를 초과하였습니다.|
|404103000|Could not find stage.|스테이지가 존재하지 않습니다.|
|404103001|Could not find stage resource.|스테이지 리소스가 존재하지 않습니다.|
|409103002|Failed to create duplicated stage name.|중복된 스테이지 이름은 생성할 수 없습니다.|
|409103003|The latest resource has already been applied.|이미 스테이지에 최신 리소스가 적용되었습니다.|
|500103000|Invalid stage resource plugin configuration.|스테이지 배포 요청에 실패했습니다. 잠시 후 다시 시도해 주세요.|
|500103001|Failed to create stage. Please try again.|스테이지 생성에 실패했습니다. 잠시 후 다시 시도해 주세요.|
|500103002|Could not find any server group.|스테이지 생성에 실패했습니다. 잠시 후 다시 시도해 주세요.|
|500103003|Failed to delete stage URL.|스테이지 삭제에 실패했습니다. 잠시 후 시도해 주세요.|
|400104000|Unable to delete base stage deploy history or the currently deployed stage deploy history.|현재 배포된 이력과 기반 배포 이력은 삭제할 수 없습니다.|
|400104001|Only possible to rollback stage for the completed deploy status.|스테이지 되돌리기를 할 수 없는 배포 상태의 이력입니다.|
|400104002|Empty stage resource for deploying.|생성된 리소스가 없어 스테이지를 생성할 수 없습니다.|
|400104003|Empty path on stage resource for deploying.|생성된 리소스가 없어 스테이지를 생성할 수 없습니다.|
|409104000|Unable to rollback stage. No difference with current stage.|이미 되돌리기가 된 배포 이력입니다.|
|409104001|Failed to deploy because current stage is deploying.|이미 스테이지 배포가 진행 중입니다.|
|409104002|Failed to deploy because stage is not changed.|이미 최신 스테이지가 배포되었습니다.|
|500104002|Failed to rollback to previous deploy data.|스테이지 배포 중 오류가 발생하여 복구를 시도했지만 복구에 실패하였습니다. 잠시 후 다시 배포를 시도해 주세요.|
|500104003|Could not find any routers for deploying.|스테이지 배포 요청에 실패했습니다. 잠시 후 다시 시도해 주세요.|
|500104004|Failed to convert stage resource list to string.|스테이지 배포 요청에 실패했습니다. 잠시 후 다시 시도해 주세요.|
|500104006|Failed to convert stage deploy JSON to stage resource list.|스테이지 배포 요청에 실패했습니다. 잠시 후 다시 시도해 주세요.|
|500104007|Failed to rollback stage.|스테이지 배포 요청에 실패했습니다. 잠시 후 다시 시도해 주세요.|
|500104008|Temporally failed to request stage deployment. Please try again later.|스테이지 배포 요청에 실패했습니다. 잠시 후 다시 시도해 주세요.|
|400105000|Failed to delete API key. The API key is in use.|연결된 API Key는 삭제할 수 없습니다. 연결을 해제한 후 삭제해 주세요.|
|404105000|Could not find API key.|API Key 정보를 찾을 수 없습니다.|
|500105000|Failed to regenerate API key.|API Key를 재발급하지 못했습니다.|
|500105001|Failed to create API key by duplicated API key.|API Key를 생성하지 못했습니다.|
|500105002|Failed to delete some API key data. Please check exception cause.|API Key 연결을 해제하지 못했습니다.|
|500105003|Failed to delete API key.|API Key를 삭제하지 못했습니다.|
|400106000|Failed to change usage plan of API key. There is no stage connected to the usage plan you want to change or it is the same as the usage plan before the change.|변경하려는 사용량 계획에 API Key가 연결 가능한 스테이지가 없습니다.|
|400106001|Failed to delete usage plan. The usage plan has a connected stage.|연결된 스테이지가 있어 사용량 계획을 삭제하지 못했습니다. 모든 스테이지를 연결 해제한 후 삭제해 주세요.|
|400106002|The stage has a connected API key. Please try after disconnecting.|스테이지에 연결된 API Key가 있습니다. API Key 연결 해제 후 스테이지를 연결 해제할 수 있습니다.|
|404106000|Could not find connected API Key.|연결된 API Key를 찾을 수 없습니다.|
|409106000|Among the requested API keys, there is an API key already connected to the stage.|연결하려는 API Key 중 스테이지에 이미 연결된 API Key가 있습니다.|
|409106001|The stage is already connected to this usage plan.|이미 사용량 계획에 연결된 스테이지입니다.|
|500106000|Failed to connect API key to usage plan stage.|일부 API Key를 연결하지 못했습니다.|
|500106001|Failed to disconnect API key from usage plan stage.|일부 API Key 연결을 해제하지 못했습니다.|
|500106002|Failed to change usage plan of API key.|API Key의 사용량 계획을 변경하지 못했습니다.|
|500106003|Failed to delete usage plan.|사용량 계획을 삭제하지 못했습니다.|
|404107000|Resource parameters can only be set on resource methods.|리소스 파라미터는 메서드에만 설정할 수 있습니다.|
|404107001|Resource parameters cannot be set on the OPTIONS method generated by CORS.|CORS에 의해 생성된 메서드에는 리소스 파라미터를 설정할 수 없습니다.|
|400108001|Failed to delete model. There is referenced model.|사용 중인 곳이 있어 모델 삭제에 실패했습니다.|
|404108000|Could not find model.|모델 정보를 찾을 수 없습니다.|
|409108000|Failed to create model by duplicated name.|이미 존재하는 모델 이름 입니다. 모델 이름은 중복될 수 없습니다.|
|404109000|Could not find API document's swagger.|API 설명서를 찾을 수 없습니다.|
|404109001|Could not find stage for making API document.|API 설명서의 게시 상태 변경에 실패했습니다.|
|500109000|Failed to convert with documentable plugin.|API 설명서 생성에 실패했습니다.|
|400110000|Invalid statistics query period.|잘못된 통계 조회 기간입니다.|
|401199000|Failed to authenticate with AppKey.|잘못된 앱키입니다.|
|500197000|Could not find recordset name.|이미 삭제된 스테이지이거나 스테이지 정보를 찾을 수 없습니다.|
