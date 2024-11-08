---
title: 대기 시간(Latency) 이해하기
slug: Web/Performance/Understanding_latency
---

{{QuickLinksWithSubPages("Web/Performance")}}

**대기 시간(Latency)** 이란 하나의 데이터 패킷이 출발지에서 도착지까지 가는 데 걸리는 시간을 뜻합니다. 성능 최적화에 있어서 대기 시간의 원인을 줄이는 것과 연결 상태가 좋지 않은 사용자를 고려하여 대기 시간이 긴 환경에서 사이트 성능을 테스트하는 것은 중요합니다. 이 글에서 대기 시간이 무엇인지, 대기 시간이 성능에 어떤 영향을 주는지, 이를 어떻게 측정하고 어떤 방법으로 줄일 수 있을지에 관해 설명합니다.

## 대기 시간이란?

대기 시간이란 일반적으로 사용자가 요청을 한 시점부터 해당 사용자에게 요청에 대한 응답을 받기까지 걸리는 시간을 말합니다. 첫 번째 요청에서 14KB 만큼의 {{glossary('DNS')}} 조회, {{glossary('TCP handshake')}}, 보안 {{glossary('TLS')}} 협상 등의 과정을 거치기 때문에 대기 시간이 깁니다. 이후의 후속 요청은 서버에 대한 연결이 이미 설정되어 있으므로 대기 시간이 줄어듭니다.

대기 시간은 네트워크나 인터넷 연결의 지연 시간을 나타냅니다. 대기 시간이 짧다는 것은 지연이 없거나 거의 없음을 의미합니다. 대기 시간이 길다는 것은 지연이 많다는 것을 의미합니다. 성능 향상의 주요 목표 중 하나는 대기 시간을 줄이는 것입니다.

기본적인 HTML 페이지와 같이 한 개의 자원에 대한 대기 시간은 사소해 보일 수 있습니다. 하지만 웹사이트는 일반적으로 여러 개의 요청을 포함합니다. HTML은 여러 개의 CSS, 스크립트, 미디어 파일에 대한 요청으로 이루어져 있기 때문입니다. 이런 요청의 개수와 크기가 커질수록 높은 대기 시간이 사용자 경험에 미치는 영향 또한 커집니다.

대기 시간이 짧은 연결에서는 요청된 자원이 거의 즉시 보입니다. 대기 시간이 긴 연결에서는 요청을 보낸 시점과 자원을 받은 시점 사이에 눈에 띄는 지연이 있습니다. 대기 시간은 데이터가 네트워크의 한 지점에서 다른 지점으로 이동하는 속도를 측정하여 얻을 수 있습니다.

대기 시간은 한 가지 방법으로 측정할 수 있는데, 예를 들면 자원에 대한 요청을 보내는 데 걸리는 시간 혹은 자원에 대한 브라우저의 요청이 다시 브라우저로 돌아오기까지 왕복 시간을 측정합니다.

## 네트워크 스로틀링

개발자 도구를 사용하여 저대역폭 네트워크 연결로 전환하면 저대역폭 네트워크의 대기 시간을 모방할 수 있습니다.

![스로틀링을 모방하여 대기 시간을 모방하기](emulate_latency.png)

개발자 도구에서 network 테이블의 스로틀링 옵션을 통해 2G, 3G 혹은 다른 대역폭으로 전환할 수 있습니다. 다양한 브라우저의 개발자 도구에는 서로 다른 사전 설정 옵션이 있으며, 모방되는 특성에는 다운로드 속도, 업로드 속도, 최소 대기 시간 또는 데이터 패킷을 보내는 데 필요한 최소 타입이 포함됩니다. 일부 사전 설정의 대략적인 값은 다음과 같습니다.

| 선택            | 다운로드 속도 | 업로드 속도 | 최소 대기 시간 (ms) |
| --------------- | ------------- | ----------- | ------------------- |
| GPRS            | 50 Kbps       | 20 Kbps     | 500                 |
| 일반적인 2G     | 250 Kbps      | 50 Kbps     | 300                 |
| 좋은 2G         | 450 Kbps      | 150 Kbps    | 150                 |
| 일반적인 3G     | 750 Kbps      | 250 Kbps    | 100                 |
| 좋은 3G         | 1.5 Mbps      | 750 Kbps    | 40                  |
| 일반적인 4G/LTE | 4 Mbps        | 3 Mbps      | 20                  |
| DSL             | 2 Mbps        | 1 Mbps      | 5                   |
| Wi-Fi           | 30 Mbps       | 15 Mbps     | 2                   |

## 네트워크 시간 측정

네트워크 탭에서 각 요청이 완료되는데 소요된 시간도 확인할 수 있습니다. 아래 사진처럼 크기가 267.5Kb인 SVG 이미지를 다운로드 받는 데 얼마나 걸렸는지 볼 수 있습니다.

![크기가 큰 SVG 이미지를 로드하는데 걸린 시간](latencymlw.png)

요청이 대기열에 있으면 네트워크 연결을 기다리는 동안 **blocked(차단)** 된 것으로 간주합니다. 차단은 하나의 서버에 동시에 너무 많은 HTTP 연결을 맺으려 할 때 발생합니다. 모든 연결이 사용 중이면 브라우저는 다른 연결이 해제될 때까지 자원을 다운로드하지 못하는데 이를 두고 요청과 자원이 차단되었다고 말합니다.

**DNS resolution** 항목은 {{glossary('DNS lookup')}} 을 수행하는 데 걸린 시간을 뜻합니다. [hostname](/ko/docs/Web/API/URL/hostname) 의 개수가 많을수록 DNS lookup 의 수행 횟수 또한 늘어납니다.

**Connecting** 항목은 {{glossary('TCP handshake')}} 을 완료하는 데 걸린 시간을 뜻합니다. 위의 DNS처럼 필요로 하는 서버 연결의 개수가 많을수록 서버와의 연결을 생성하는데 걸리는 시간 또한 늘어납니다.

**{{glossary('TLS')}} handshake** 항목은 보안 연결을 수립하는 데 걸린 시간을 뜻합니다. 물론 TLS handshake 는 안전하지 않은 연결보다 연결하는데 오래 걸리지만 그만큼의 시간은 안전한 연결을 위해 투자할 가치가 있습니다.

**Sending** 항목은 HTTP 요청을 서버로 전송하는데 걸린 시간을 뜻합니다.

**Waiting** 항목은 디스크 대기 시간으로, 서버가 응답을 완료하는데 걸린 시간을 뜻합니다. 디스크 대기 시간은 성능 문제의 주요 원인이었지만 컴퓨터 메모리와 CPU의 발전에 따라 서버의 성능 또한 개선되었습니다. 서버가 수행해야 하는 일의 복잡도에 따라 이 항목은 여전히 문제가 될 수도 있습니다.

**Receiving** 항목은 자원을 다운로드 받는 데 걸린 시간을 뜻합니다. Receiving 시간은 네트워크 용량과 자원 파일의 크기에 따라 결정됩니다. 이미지가 캐싱되었다면 즉각적으로 완료되었을 수 있고, 스로틀링이 걸렸다면 43초가 걸렸을 수도 있습니다!

## 대기 시간 측정

**Network latency** 란 데이터 요청이 요청을 작성하는 컴퓨터에서 응답하는 컴퓨터에 도달하는 데 걸리는 시간을 말합니다. 이는 데이터가 응답하는 컴퓨터에서 요청한 컴퓨터로 다시 돌아오는 시간을 포함합니다. 일반적으로 왕복 지연으로 측정됩니다.

**Disk latency** 란 컴퓨터(일반적으로 서버)가 요청을 수신한 시점부터 응답을 반환하기까지 걸린 시간을 말합니다.