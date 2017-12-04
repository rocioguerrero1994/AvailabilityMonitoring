---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 화이트리스트 및 블랙리스트에서 블로킹 및 필터링
{: #avmon_filters}

화이트리스트 및 블랙리스트를 사용하여 요청이 전송될 대상 리소스 및 애플리케이션 테스트의 메트릭과 상태에 컨트리뷰션하는 리소스를 판별할 수 있습니다. 화이트리스트 및 블랙리스트는 웹 페이지 및 스크립팅된 작동 테스트에만 사용 가능합니다.
{: shortdesc}

**화이트리스트** 및 **블랙리스트** 필드는 테스트가 액세스할 수 있는 또는 액세스할 수 없는 리소스 및 테스트의 메트릭과 상태에 컨트리뷰션하는 리소스를 정의합니다. 화이트리스트 및 블랙리스트는 써드파티 메트릭 등과 같은 테스트된 웹 애플리케이션의 응답 시간에 컨트리뷰션하는 리소스 및 종속 항목을 제어할 수 있습니다. 웹 페이지 또는 스크립팅된 작동 테스트를 작성할 때 화이트리스트 및 블랙리스트를 구성할 수 있습니다. 

**화이트리스트**를 사용하여 허용된 도메인 및 URL을 정의한 후에 **블랙리스트**를 사용하여 허용된 위치의 특정 요소를 차단할 수 있습니다. 

## 구문

블랙리스트 및 화이트리스트의 항목을 분리하려면 쉼표(,)를 사용하십시오. 각 URL 또는 도메인의 요소를 필터링하려면 와일드카드 기호(\*)를 사용하십시오. 

## 화이트리스트

화이트리스트 필드에 요청 및 메트릭 계산에 포함할 URL 또는 도메인을 추가하십시오. 화이트리스트에서 최대 10개의 항목을 나열할 수 있습니다. 각 항목 길이는 200자를 초과할 수 없습니다. 화이트리스트의 항목과 일치하지 않는 모든 도메인 및 URL은 차단됩니다. 

예:
```
ibm.com, *developerworks*, *.s81c.com/*
```
{: codeblock}

## 블랙리스트

블랙리스트 필드에 요청 및 메트릭 계산에서 차단할 URL 또는 도메인을 추가하십시오. 블랙리스트에서 최대 20개의 항목을 나열할 수 있습니다. 각 항목 길이는 200자를 초과할 수 없습니다. 

예:
```
*.profile.*.cloudfront.net/*.png
```
{: codeblock}

## 필터링 및 블로킹 작동

테스트는 화이트리스트 및 블랙리스트 모두를 보유할 수 있습니다. 허용 또는 차단되는 위치를 판별할 때 블랙리스트는 항상 화이트리스트를 대체합니다. 다음 테이블에는 화이트리스트 및 블랙리스트가 포함된 모든 시나리오에 대한 필터링 및 블로킹 작동이 표시되어 있습니다. 

<table id="avmon_whitelist_blacklist__table_gyg_vvp_fbb">
<caption>테이블 1. 화이트리스트 및 블랙리스트에 대한 필터링 및 블로킹 작동</caption>
<thead>
<tr>
<th>블랙리스트</th>
<th>화이트리스트</th>
<th>동작</th>
<th>이유</th>
</tr>
</thead>
<tbody>
<tr>
<td>비어 있음</td>
<td>비어 있음</td>
<td>액세스 허용</td>
<td>필터링 규칙이 입력되지 않았습니다.</td>
</tr>
<tr>
<td>비어 있음</td>
<td>URL이 목록 항목과 일치하지 않음</td>
<td>액세스 차단</td>
<td>URL이 화이트리스트에 없습니다.</td>
</tr>
<tr>
<td>비어 있음</td>
<td>URL이 목록 항목과 일치함</td>
<td>액세스 허용</td>
<td>URL이 화이트리스트에 있습니다. 액세스를 차단할 블랙리스트 항목이 없습니다. </td>
</tr>
<tr>
<td>URL이 목록 항목과 일치하지 않음</td>
<td>비어 있음</td>
<td>액세스 허용</td>
<td>URL이 블랙리스트에 없습니다.액세스를 차단할 화이트리스트 항목이 없습니다. </td>
</tr>
<tr>
<td>URL이 목록 항목과 일치함</td>
<td>비어 있음</td>
<td>액세스 차단</td>
<td>URL이 블랙리스트에 있습니다.</td>
</tr>
<tr>
<td>URL이 목록 항목과 일치하지 않음</td>
<td>URL이 목록 항목과 일치하지 않음</td>
<td>액세스 차단</td>
<td>URL이 화이트리스트에 없습니다.</td>
</tr>
<tr>
<td>URL이 목록 항목과 일치하지 않음</td>
<td>URL이 목록 항목과 일치함</td>
<td>액세스 허용</td>
<td>URL이 화이트리스트에 있습니다. URL이 블랙리스트에 없습니다.</td>
</tr>
<tr>
<td>URL이 목록 항목과 일치함</td>
<td>URL이 목록 항목과 일치하지 않음</td>
<td>액세스 차단</td>
<td>URL이 화이트리스트에 없습니다.URL이 블랙리스트에 있습니다.</td>
</tr>
<tr>
<td>URL이 목록 항목과 일치함</td>
<td>URL이 목록 항목과 일치함</td>
<td>액세스 차단</td>
<td>URL이 블랙리스트에 있습니다.블랙리스트 항목이 화이트리스트 항목을 대체합니다. </td>
</tr>
</tbody>
</table>