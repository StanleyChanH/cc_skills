# Crewai - Api

**Pages:** 55

---

## `SerpApiGoogleShoppingTool`

**URL:** llms-txt#`serpapigoogleshoppingtool`

**Contents:**
- Description
- Installation
- Environment Variables
- Example
- Notes
- Parameters
  - Run Parameters

Leverage `SerpApiGoogleShoppingTool` to query Google Shopping via SerpApi and retrieve product-oriented results.

## Environment Variables

* `SERPAPI_API_KEY` (required): API key for SerpApi. Create one at [https://serpapi.com/](https://serpapi.com/) (free tier available).

* Set `SERPAPI_API_KEY` in the environment. Create a key at [https://serpapi.com/](https://serpapi.com/)
* See also Google Web Search via SerpApi: `/en/tools/search-research/serpapi-googlesearchtool`

* `search_query` (str, required): Product search query.
* `location` (str, optional): Geographic location parameter.

**Examples:**

Example 1 (unknown):
```unknown
## Environment Variables

* `SERPAPI_API_KEY` (required): API key for SerpApi. Create one at [https://serpapi.com/](https://serpapi.com/) (free tier available).

## Example
```

---

## SerpApi 구글 검색 도구

**URL:** llms-txt#serpapi-구글-검색-도구

Source: https://docs.crewai.com/ko/tools/search-research/serpapi-googlesearchtool

SerpApiGoogleSearchTool은 SerpApi 서비스를 사용하여 구글 검색을 수행합니다.

---

## Zapier 트리거

**URL:** llms-txt#zapier-트리거

**Contents:**
- 사전 요구 사항
- 단계별 설정
- 성공을 위한 팁

Source: https://docs.crewai.com/ko/enterprise/guides/zapier-trigger

Zapier 워크플로우에서 CrewAI crew를 트리거하여 앱 간 워크플로우를 자동화합니다

이 가이드는 CrewAI AMP용 Zapier 트리거를 설정하는 과정을 안내합니다. 이를 통해 CrewAI AMP와 기타 애플리케이션 간의 워크플로우를 자동화할 수 있습니다.

* CrewAI AMP 계정
* Zapier 계정
* Slack 계정 (이 특정 예시에 해당)

<Steps>
  <Step title="Slack 트리거 설정">
    * Zapier에서 새 Zap을 만듭니다.

<Frame>
      <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-1.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=d7602ce90ddcd4f0365fd821f4ff1ff2" alt="Zapier 1" data-og-width="621" width="621" data-og-height="463" height="463" data-path="images/enterprise/zapier-1.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-1.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=3682030aedc56484321e678fe075bd97 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-1.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=cf755fd940ed2e79378b91369e620cd9 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-1.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=e2fc3de247c9054220b0255a1544b160 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-1.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=6f10592fc96a7ea63bbd8548328c8cea 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-1.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=ab8d3cce86244b055400ad4ecf60d51d 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-1.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=37b9df91c5efb53fd1d6c9a7fc34c624 2500w" />
    </Frame>
  </Step>

<Step title="트리거 앱으로 Slack 선택">
    <Frame>
      <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-2.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=e5cdc5705b87b4e06178fa12fb5ef64b" alt="Zapier 2" data-og-width="670" width="670" data-og-height="684" height="684" data-path="images/enterprise/zapier-2.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-2.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=f5d12f107504be7a7521ddf91d9ec413 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-2.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=bebe1ccb4e8d4b4d077d4039b5a8c419 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-2.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=edb0a91b6ed81fc58470f998b3329978 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-2.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=262296a5be2e6762da49b77fcd9bd5e2 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-2.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=40b91cfb93939c2dd0b3f6222b376f90 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-2.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=18bd414e6d18ec375cf94d94d2510775 2500w" />
    </Frame>

* 트리거 이벤트로 `New Pushed Message`를 선택합니다.
    * 아직 Slack 계정을 연결하지 않았다면 연결하세요.
  </Step>

<Step title="CrewAI AMP 액션 구성">
    * Zap에 새 액션 단계를 추가합니다.
    * CrewAI+를 액션 앱으로, Kickoff를 액션 이벤트로 선택합니다.

<Frame>
      <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-3.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=e52e2404a73623df30d125873bd8ff42" alt="Zapier 5" data-og-width="670" width="670" data-og-height="670" height="670" data-path="images/enterprise/zapier-3.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-3.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=786eec1ccf1fa275c710cd3f35d7c955 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-3.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=bffb3ef5cd02ccd103a070893842ce2a 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-3.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=20c3a2004d6186a7217d6492f093dde5 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-3.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=3563e2fede93f6c678e6e25269a4781f 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-3.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=1641552fd6d8e6b477875ab53bd6f401 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-3.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=6c227ade8128df087cd958a98a398605 2500w" />
    </Frame>
  </Step>

<Step title="CrewAI AMP 계정 연결">
    * CrewAI AMP 계정을 연결하세요.
    * 워크플로에 적합한 Crew를 선택하세요.

<Frame>
      <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-4.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=13aac37fdb67ee1c9f841a602ac3abf5" alt="Zapier 6" data-og-width="670" width="670" data-og-height="657" height="657" data-path="images/enterprise/zapier-4.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-4.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=ad12e0febda29f3e6b68a245b83f17bd 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-4.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=08ff0773ed36f8fbb1c33acd90a50f79 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-4.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=cf788ee6daea3ef786b456c7a80d79a5 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-4.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=b5a14e7f332b6ebef8131f6a26835417 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-4.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=f0b27340ce1a510f990a305674d53107 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-4.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=061132e0ca03b82737f62cd4a113b12c 2500w" />
    </Frame>

* Slack 메시지의 데이터를 사용하여 Crew의 입력값을 구성하세요.
  </Step>

<Step title="CrewAI AMP 출력 포맷팅">
    * CrewAI AMP에서 출력된 텍스트를 포맷팅하기 위해 추가 액션 단계를 추가합니다.
    * Zapier의 포매팅 도구를 사용하여 Markdown 출력을 HTML로 변환합니다.

<Frame>
      <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-5.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=e772b4803dfffe4de12d9a7ea21484ce" alt="Zapier 8" data-og-width="670" width="670" data-og-height="674" height="674" data-path="images/enterprise/zapier-5.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-5.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=d3de75f0a0d65af30620c7d9b89a1802 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-5.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=42ec43489c3e07aea4f64790efad63ef 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-5.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=68f473bd4c78acb0422d724a8dc9ac27 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-5.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=d3149ba4fc03d00e00f81e6774dd4253 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-5.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=ea05c3790b67091e18e32291c2ecceae 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-5.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=a7519c4547a79061828c08d71091ac18 2500w" />
    </Frame>

<Frame>
      <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-6.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=9fa4a34d5c511b6bb76f276348928699" alt="Zapier 9" data-og-width="670" width="670" data-og-height="675" height="675" data-path="images/enterprise/zapier-6.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-6.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=722c246b4c43b099734105a8c57e094c 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-6.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=91bfde61dfceb3998b85a0fd947b8f1b 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-6.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=d56af89fb61384149deef33e22b57bfe 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-6.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=d9097a2e0d8ddf13f0d17c7f65d4a263 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-6.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=59e5ad6b6f94117c4bdb264cde97a5ff 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-6.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=edf53161c63e0daf6e3e61abf1b1a265 2500w" />
    </Frame>
  </Step>

<Step title="출력 이메일로 전송">
    * 포맷팅된 출력을 이메일로 전송하는 마지막 액션 단계를 추가합니다.
    * 원하는 이메일 서비스를 선택하세요 (예: Gmail, Outlook).
    * 수신자, 제목, 본문 등 이메일 상세 정보를 구성하세요.
    * 포맷팅된 CrewAI AMP 출력을 이메일 본문에 삽입합니다.

<Frame>
      <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=f3d2a0c67b29888cfdc5b0d81ba5c29b" alt="Zapier 7" data-og-width="670" width="670" data-og-height="673" height="673" data-path="images/enterprise/zapier-7.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=399cf0c5f81cbf170a3c8d4d8557b37f 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=8b6c488f27b8797c575a711f9b257b81 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=f905970cb40554fe1c3674afa7f2209e 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=92ee968916226d374826eb358c264f66 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=1853357f43dd7032c890fd3a57fbd99e 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=9c5e507725c754d90937f0b7b1ee7699 2500w" />
    </Frame>
  </Step>

<Step title="Slack에서 crew 실행">
    * Slack 채널에 텍스트를 입력하세요.

<Frame>
      <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7b.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=916dbdffd171dc52c40ebc74cc39a38f" alt="Zapier 10" data-og-width="509" width="509" data-og-height="85" height="85" data-path="images/enterprise/zapier-7b.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7b.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=fce126149004d422a866d0e9ae00b9b0 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7b.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=c051b11bd9e2fd2db9a0fbd0997043cd 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7b.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=2f14112b9c9551239a1b82bd220b85fa 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7b.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=f302f0da373ef859e49ca1b4a7540b94 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7b.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=386dfa4b1f1f4005e705771b39c1ec33 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-7b.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=57c6a7727031de0aebbdbeb65a03e27c 2500w" />
    </Frame>

* 3점 버튼을 선택한 후 'Push to Zapier'를 선택하세요.

<Frame>
      <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-8.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=a6a6e2fd0b0b239af4c17ae1f34ad720" alt="Zapier 11" data-og-width="405" width="405" data-og-height="260" height="260" data-path="images/enterprise/zapier-8.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-8.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=e9bb5078ea66e8e7774b262caea53295 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-8.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=ec7f588235922fd96b8aea884cba1221 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-8.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=d82c4c5d979814febba30bbfdeb2831d 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-8.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=7a8f97770f17f96b4585c1b38b000fb8 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-8.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=e8bae8057f2a294c977f7d568660f915 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/zapier-8.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=301cbedee7d42601db44f3710755653c 2500w" />
    </Frame>
  </Step>

<Step title="crew 선택 후 Kick Off로 Push">
    <Frame>
      <img src="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/enterprise/zapier-9.png?fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=eda865381d7121d38025c2b13abeccdf" alt="Zapier 12" data-og-width="659" width="659" data-og-height="531" height="531" data-path="images/enterprise/zapier-9.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/enterprise/zapier-9.png?w=280&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=283165c2ef289340b66aa9ed1719f97d 280w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/enterprise/zapier-9.png?w=560&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=d28641bc16596826f13a9d14ac0a2f2b 560w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/enterprise/zapier-9.png?w=840&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=e68731bab42671ec59dfd179c210bd80 840w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/enterprise/zapier-9.png?w=1100&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=234f5bffd3865f2a15d744455fef0c90 1100w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/enterprise/zapier-9.png?w=1650&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=d59b16a7bfbdf3b07d696ef70be0a31a 1650w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/enterprise/zapier-9.png?w=2500&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=1669d1af7e28868e5f260df18b36dd49 2500w" />
    </Frame>
  </Step>
</Steps>

* CrewAI AMP 입력값이 Slack 메시지에서 올바르게 매핑되었는지 확인하세요.
* Zap을 활성화하기 전에 철저히 테스트하여 잠재적인 문제를 미리 파악하세요.
* 워크플로우 내에서 발생할 수 있는 실패 상황을 관리하기 위해 오류 처리 단계를 추가하는 것을 고려하세요.

이 단계를 따르면 Slack 메시지로 트리거되는 자동화된 워크플로우와 CrewAI AMP 출력이 포함된 이메일 알림을 설정할 수 있습니다.

---

## Initialize the tool with your API keys using a context manager

**URL:** llms-txt#initialize-the-tool-with-your-api-keys-using-a-context-manager

with StagehandTool(
    api_key="your-browserbase-api-key",
    project_id="your-browserbase-project-id",
    model_api_key="your-llm-api-key",  # OpenAI or Anthropic API key
    model_name=AvailableModel.CLAUDE_3_7_SONNET_LATEST,  # Optional: specify which model to use
) as stagehand_tool:
    # Create an agent with the tool
    researcher = Agent(
        role="Web Researcher",
        goal="Find and summarize information from websites",
        backstory="I'm an expert at finding information online.",
        verbose=True,
        tools=[stagehand_tool],
    )

# Create a task that uses the tool
    research_task = Task(
        description="Go to https://www.example.com and tell me what you see on the homepage.",
        agent=researcher,
    )

# Run the crew
    crew = Crew(
        agents=[researcher],
        tasks=[research_task],
        verbose=True,
    )

result = crew.kickoff()
    print(result)
python  theme={null}
from crewai import Agent, Task, Crew
from crewai_tools import StagehandTool
from stagehand.schemas import AvailableModel

**Examples:**

Example 1 (unknown):
```unknown
#### 2. Gerenciamento Manual de Recursos
```

---

## Ensure TAVILY_API_KEY is set in your environment

**URL:** llms-txt#ensure-tavily_api_key-is-set-in-your-environment

---

## Adicione a chave de API do seu provedor também.

**URL:** llms-txt#adicione-a-chave-de-api-do-seu-provedor-também.

**Contents:**
- Passo 8: Instale as Dependências
- Passo 9: Execute sua Crew
- Passo 10: Revise o Resultado
- Explorando Outros Comandos da CLI

bash  theme={null}
crewai install
bash  theme={null}
crewai run
bash  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
Confira o [guia de configuração do LLM](/pt-BR/concepts/llms#setting-up-your-llm) para detalhes sobre como configurar o provedor de sua escolha. Você pode obter a chave da Serper em [Serper.dev](https://serper.dev/).

## Passo 8: Instale as Dependências

Instale as dependências necessárias usando a CLI da CrewAI:
```

Example 2 (unknown):
```unknown
Este comando irá:

1. Ler as dependências da configuração do seu projeto
2. Criar um ambiente virtual se necessário
3. Instalar todos os pacotes necessários

## Passo 9: Execute sua Crew

Agora chega o momento empolgante – é hora de rodar sua crew e assistir à colaboração de IA em ação!
```

Example 3 (unknown):
```unknown
Ao rodar esse comando, você verá sua crew ganhando vida. O pesquisador irá coletar informações sobre o tema especificado, e o analista irá criar um relatório abrangente baseado nessa pesquisa. Você poderá acompanhar em tempo real o raciocínio, as ações e os resultados dos agentes à medida que colaboram para concluir as tarefas.

## Passo 10: Revise o Resultado

Após a conclusão do trabalho da crew, você encontrará o relatório final em `output/report.md`. O relatório incluirá:

1. Um resumo executivo
2. Informações detalhadas sobre o tema
3. Análises e insights
4. Recomendações ou considerações futuras

Tire um momento para valorizar o que você realizou – você criou um sistema no qual múltiplos agentes de IA colaboraram em uma tarefa complexa, cada um contribuindo com suas habilidades especializadas para gerar um resultado maior do que qualquer agente conseguiria sozinho.

## Explorando Outros Comandos da CLI

A CrewAI oferece vários outros comandos úteis de CLI para trabalhar com crews:
```

---

## Apify Actors

**URL:** llms-txt#apify-actors

Source: https://docs.crewai.com/pt-BR/tools/automation/apifyactorstool

`ApifyActorsTool` permite que você execute Apify Actors para adicionar recursos de raspagem de dados na web, coleta, extração de dados e automação web aos seus fluxos de trabalho CrewAI.

---

## SerpApi Google Shopping Tool

**URL:** llms-txt#serpapi-google-shopping-tool

Source: https://docs.crewai.com/pt-BR/tools/search-research/serpapi-googleshoppingtool

The `SerpApiGoogleShoppingTool` searches Google Shopping results using SerpApi.

---

## POST /kickoff

**URL:** llms-txt#post-/kickoff

Source: https://docs.crewai.com/pt-BR/api-reference/kickoff

enterprise-api.pt-BR.yaml post /kickoff
Iniciar a execução da crew

---

## Configure as chaves de API

**URL:** llms-txt#configure-as-chaves-de-api

os.environ["SERPER_API_KEY"] = "Your Key" # chave da API serper.dev
os.environ["OPENAI_API_KEY"] = "Your Key"

---

## Initialize the tool with your API key

**URL:** llms-txt#initialize-the-tool-with-your-api-key

tool = HyperbrowserLoadTool(api_key="your_api_key")  # Or use environment variable

---

## Set API keys for tool initialization

**URL:** llms-txt#set-api-keys-for-tool-initialization

os.environ["OPENAI_API_KEY"] = "Your Key"
os.environ["SERPER_API_KEY"] = "Your Key"

---

## SERPER_API_KEY=<your api key>

**URL:** llms-txt#serper_api_key=<your-api-key>

search = GoogleSerperAPIWrapper()

class SearchTool(BaseTool):
    name: str = "Search"
    description: str = "Useful for search-based queries. Use this to find current information about markets, companies, and trends."
    search: GoogleSerperAPIWrapper = Field(default_factory=GoogleSerperAPIWrapper)

def _run(self, query: str) -> str:
        """Execute the search query and return results"""
        try:
            return self.search.run(query)
        except Exception as e:
            return f"Error performing search: {str(e)}"

---

## Armazenar chaves API em variáveis de ambiente

**URL:** llms-txt#armazenar-chaves-api-em-variáveis-de-ambiente

**Contents:**
  - 3. Planejar para Falhas de Servidor

exa_key = os.getenv("EXA_API_KEY")
exa_profile = os.getenv("EXA_PROFILE")

agente = Agent(
    role="Agente Seguro",
    goal="Usar ferramentas MCP com segurança",
    backstory="Agente consciente da segurança",
    mcps=[f"https://mcp.exa.ai/mcp?api_key={exa_key}&profile={exa_profile}"]
)
python  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
### 3. Planejar para Falhas de Servidor
```

---

## Exemplo de uso da API Kickoff com webhooks

**URL:** llms-txt#exemplo-de-uso-da-api-kickoff-com-webhooks

**Contents:**
- Formato do Webhook

Se `realtime` estiver definido como `true`, cada evento será entregue individualmente e imediatamente, com impacto no desempenho da crew/flow.

## Formato do Webhook

Cada webhook envia uma lista de eventos:

---

## Inicialize a ferramenta com um Apify Actor

**URL:** llms-txt#inicialize-a-ferramenta-com-um-apify-actor

tool = ApifyActorsTool(actor_name="apify/rag-web-browser")

---

## Zapier 액션 도구

**URL:** llms-txt#zapier-액션-도구

Source: https://docs.crewai.com/ko/tools/automation/zapieractionstool

ZapierActionsAdapter는 Zapier 액션을 CrewAI 도구로 노출하여 자동화를 지원합니다.

---

## os.environ["TAVILY_API_KEY"] = "YOUR_API_KEY"

**URL:** llms-txt#os.environ["tavily_api_key"]-=-"your_api_key"

---

## Obtenha as chaves de API para os serviços

**URL:** llms-txt#obtenha-as-chaves-de-api-para-os-serviços

OPENAI_API_KEY = getpass("🔑 Digite sua OpenAI API key: ")
SERPER_API_KEY = getpass("🔑 Digite sua Serper API key: ")

---

## Maxim API Configuration

**URL:** llms-txt#maxim-api-configuration

**Contents:**
  - 2. 필수 패키지 임포트하기
  - 3. API 키로 Maxim 초기화하기

MAXIM_API_KEY=your_api_key_here
MAXIM_LOG_REPO_ID=your_repo_id_here
python  theme={null}
from crewai import Agent, Task, Crew, Process
from maxim import Maxim
from maxim.logger.crewai import instrument_crewai
python {8} theme={null}

**Examples:**

Example 1 (unknown):
```unknown
### 2. 필수 패키지 임포트하기
```

Example 2 (unknown):
```unknown
### 3. API 키로 Maxim 초기화하기
```

---

## ✅ Use these naming patterns instead

**URL:** llms-txt#✅-use-these-naming-patterns-instead

**Contents:**
  - Best Practices
  - Interact with Your Deployed Crew
  - Trigger an Execution
  - Monitoring and Analytics
  - Advanced Features

OPENAI_API_KEY=sk-...
DATABASE_CREDENTIALS=mypassword
API_CONFIG=secret123
```

1. **Use standard naming conventions**: `PROVIDER_API_KEY` instead of `PROVIDER_TOKEN`
2. **Test locally first**: Ensure your crew works with the renamed variables
3. **Update your code**: Change any references to the old variable names
4. **Document changes**: Keep track of renamed variables for your team

<Tip>
  If you encounter deployment failures with cryptic environment variable errors, check your variable names against these patterns first.
</Tip>

### Interact with Your Deployed Crew

Once deployment is complete, you can access your crew through:

1. **REST API**: The platform generates a unique HTTPS endpoint with these key routes:
   * `/inputs`: Lists the required input parameters
   * `/kickoff`: Initiates an execution with provided inputs
   * `/status/{kickoff_id}`: Checks the execution status

2. **Web Interface**: Visit [app.crewai.com](https://app.crewai.com) to access:
   * **Status tab**: View deployment information, API endpoint details, and authentication token
   * **Run tab**: Visual representation of your crew's structure
   * **Executions tab**: History of all executions
   * **Metrics tab**: Performance analytics
   * **Traces tab**: Detailed execution insights

### Trigger an Execution

From the Enterprise dashboard, you can:

1. Click on your crew's name to open its details
2. Select "Trigger Crew" from the management interface
3. Enter the required inputs in the modal that appears
4. Monitor progress as the execution moves through the pipeline

### Monitoring and Analytics

The Enterprise platform provides comprehensive observability features:

* **Execution Management**: Track active and completed runs
* **Traces**: Detailed breakdowns of each execution
* **Metrics**: Token usage, execution times, and costs
* **Timeline View**: Visual representation of task sequences

### Advanced Features

The Enterprise platform also offers:

* **Environment Variables Management**: Securely store and manage API keys
* **LLM Connections**: Configure integrations with various LLM providers
* **Custom Tools Repository**: Create, share, and install tools
* **Crew Studio**: Build crews through a chat interface without writing code

<Card title="Need Help?" icon="headset" href="mailto:support@crewai.com">
  Contact our support team for assistance with deployment issues or questions about the Enterprise platform.
</Card>

---

## Inicialize a ferramenta com a chave da API do Browserbase e o Project ID

**URL:** llms-txt#inicialize-a-ferramenta-com-a-chave-da-api-do-browserbase-e-o-project-id

**Contents:**
- Argumentos

tool = BrowserbaseLoadTool()
```

Os parâmetros a seguir podem ser usados para customizar o comportamento do `BrowserbaseLoadTool`:

| Argumento         | Tipo     | Descrição                                                                                        |
| :---------------- | :------- | :----------------------------------------------------------------------------------------------- |
| **api\_key**      | `string` | *Opcional*. Chave de API do Browserbase. Padrão é a variável de ambiente `BROWSERBASE_API_KEY`.  |
| **project\_id**   | `string` | *Opcional*. Project ID do Browserbase. Padrão é a variável de ambiente `BROWSERBASE_PROJECT_ID`. |
| **text\_content** | `bool`   | *Opcional*. Recuperar somente o conteúdo em texto. O padrão é `False`.                           |
| **session\_id**   | `string` | *Opcional*. Forneça um Session ID existente.                                                     |
| **proxy**         | `bool`   | *Opcional*. Habilitar/Desabilitar proxies. O padrão é `False`.                                   |

---

## Defina as chaves de API para inicialização da ferramenta

**URL:** llms-txt#defina-as-chaves-de-api-para-inicialização-da-ferramenta

os.environ["OPENAI_API_KEY"] = "Sua Chave"
os.environ["SERPER_API_KEY"] = "Sua Chave"

---

## Obter chaves de API para serviços

**URL:** llms-txt#obter-chaves-de-api-para-serviços

OPENAI_API_KEY = getpass("🔑 Digite sua chave de API do OpenAI: ")

---

## GET /inputs

**URL:** llms-txt#get-/inputs

Source: https://docs.crewai.com/pt-BR/api-reference/inputs

enterprise-api.pt-BR.yaml get /inputs
Obter entradas necessárias para sua crew

---

## Ensure the TAVILY_API_KEY environment variable is set

**URL:** llms-txt#ensure-the-tavily_api_key-environment-variable-is-set

---

## Apify 액터

**URL:** llms-txt#apify-액터

Source: https://docs.crewai.com/ko/tools/automation/apifyactorstool

`ApifyActorsTool`을(를) 사용하면 Apify 액터를 호출하여 CrewAI 워크플로우에 웹 스크래핑, 크롤링, 데이터 추출 및 웹 자동화 기능을 제공할 수 있습니다.

---

## `SeleniumScrapingTool`

**URL:** llms-txt#`seleniumscrapingtool`

**Contents:**
- Descrição
- Instalação
- Exemplo

<Note>
  Esta ferramenta está atualmente em desenvolvimento. Conforme aprimoramos suas capacidades, os usuários podem encontrar comportamentos inesperados.
  Seu feedback é inestimável para que possamos melhorar.
</Note>

O `SeleniumScrapingTool` foi criado para tarefas de raspagem web de alta eficiência.
Permite a extração precisa de conteúdo de páginas web utilizando seletores CSS para direcionar elementos específicos.
Seu design atende a uma ampla gama de necessidades de scraping, oferecendo flexibilidade para trabalhar com qualquer URL de site fornecida.

Para utilizar esta ferramenta, é necessário instalar o pacote CrewAI tools e o Selenium:

Você também precisará ter o Chrome instalado em seu sistema, pois a ferramenta utiliza o Chrome WebDriver para automação do navegador.

O exemplo a seguir demonstra como usar o `SeleniumScrapingTool` com um agente CrewAI:

```python Code theme={null}
from crewai import Agent, Task, Crew, Process
from crewai_tools import SeleniumScrapingTool

**Examples:**

Example 1 (unknown):
```unknown
Você também precisará ter o Chrome instalado em seu sistema, pois a ferramenta utiliza o Chrome WebDriver para automação do navegador.

## Exemplo

O exemplo a seguir demonstra como usar o `SeleniumScrapingTool` com um agente CrewAI:
```

---

## "asp": True,  # Bypass scraping blocking solutions, like Cloudflare

**URL:** llms-txt#"asp":-true,--#-bypass-scraping-blocking-solutions,-like-cloudflare

---

## Configuração da API Maxim

**URL:** llms-txt#configuração-da-api-maxim

**Contents:**
  - 2. Importe os pacotes necessários
  - 3. Inicialize o Maxim com sua chave de API

MAXIM_API_KEY=your_api_key_here
MAXIM_LOG_REPO_ID=your_repo_id_here
python  theme={null}
from crewai import Agent, Task, Crew, Process
from maxim import Maxim
from maxim.logger.crewai import instrument_crewai
python  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
### 2. Importe os pacotes necessários
```

Example 2 (unknown):
```unknown
### 3. Inicialize o Maxim com sua chave de API
```

---

## Initialize the tool with your API keys

**URL:** llms-txt#initialize-the-tool-with-your-api-keys

**Contents:**
- Tipos de Comando
  - 1. Comando Act

stagehand_tool = StagehandTool(
    api_key="your-browserbase-api-key",
    project_id="your-browserbase-project-id",
    model_api_key="your-llm-api-key",
    model_name=AvailableModel.CLAUDE_3_7_SONNET_LATEST,
)

try:
    # Create an agent with the tool
    researcher = Agent(
        role="Web Researcher",
        goal="Find and summarize information from websites",
        backstory="I'm an expert at finding information online.",
        verbose=True,
        tools=[stagehand_tool],
    )

# Create a task that uses the tool
    research_task = Task(
        description="Go to https://www.example.com and tell me what you see on the homepage.",
        agent=researcher,
    )

# Run the crew
    crew = Crew(
        agents=[researcher],
        tasks=[research_task],
        verbose=True,
    )

result = crew.kickoff()
    print(result)
finally:
    # Explicitly clean up resources
    stagehand_tool.close()
python  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
## Tipos de Comando

A StagehandTool suporta três tipos diferentes de comando para tarefas específicas de automação web:

### 1. Comando Act

O tipo de comando `act` (padrão) permite interações em páginas web como clicar em botões, preencher formulários e navegar.
```

---

## GET /status/{kickoff_id}

**URL:** llms-txt#get-/status/{kickoff_id}

Source: https://docs.crewai.com/pt-BR/api-reference/status

enterprise-api.pt-BR.yaml get /status/{kickoff_id}
Obter o status da execução

---

## Example with custom scraping parameters

**URL:** llms-txt#example-with-custom-scraping-parameters

web_scraper_agent = Agent(
    role="Web Scraper",
    goal="Extract information from websites with custom parameters",
    backstory="An expert in web scraping who can extract content from any website.",
    tools=[scrape_tool],
    verbose=True,
)

---

## POST /resume

**URL:** llms-txt#post-/resume

Source: https://docs.crewai.com/pt-BR/api-reference/resume

enterprise-api.pt-BR.yaml post /resume
Retomar execução do crew com feedback humano

---

## `SerpApiGoogleSearchTool`

**URL:** llms-txt#`serpapigooglesearchtool`

**Contents:**
- Description
- Installation
- Environment Variables
- Example
- Notes
- Parameters
  - Run Parameters
- Notes

Use the `SerpApiGoogleSearchTool` to run Google searches with SerpApi and retrieve structured results. Requires a SerpApi API key.

## Environment Variables

* `SERPAPI_API_KEY` (required): API key for SerpApi. Create one at [https://serpapi.com/](https://serpapi.com/) (free tier available).

* Set `SERPAPI_API_KEY` in the environment. Create a key at [https://serpapi.com/](https://serpapi.com/)
* See also Google Shopping via SerpApi: `/en/tools/search-research/serpapi-googleshoppingtool`

* `search_query` (str, required): The Google query.
* `location` (str, optional): Geographic location parameter.

* This tool wraps SerpApi and returns structured search results.

**Examples:**

Example 1 (unknown):
```unknown
## Environment Variables

* `SERPAPI_API_KEY` (required): API key for SerpApi. Create one at [https://serpapi.com/](https://serpapi.com/) (free tier available).

## Example
```

---

## `ApifyActorsTool`

**URL:** llms-txt#`apifyactorstool`

**Contents:**
- Descrição
- Passos para começar
- Exemplo de uso

Integre [Apify Actors](https://apify.com/actors) nos seus fluxos de trabalho CrewAI.

O `ApifyActorsTool` conecta [Apify Actors](https://apify.com/actors), programas em nuvem para raspagem e automação web, aos seus fluxos de trabalho CrewAI.
Utilize qualquer um dos mais de 4.000 Actors disponíveis na [Apify Store](https://apify.com/store) para casos de uso como extração de dados de redes sociais, motores de busca, mapas online, sites de e-commerce, portais de viagem ou sites em geral.

Para mais detalhes, consulte a [integração Apify CrewAI](https://docs.apify.com/platform/integrations/crewai) na documentação do Apify.

## Passos para começar

<Steps>
  <Step title="Instale as dependências">
    Instale `crewai[tools]` e `langchain-apify` usando pip: `pip install 'crewai[tools]' langchain-apify`.
  </Step>

<Step title="Obtenha um token de API do Apify">
    Cadastre-se no [Apify Console](https://console.apify.com/) e obtenha seu [token de API do Apify](https://console.apify.com/settings/integrations).
  </Step>

<Step title="Configure o ambiente">
    Defina seu token de API do Apify na variável de ambiente `APIFY_API_TOKEN` para habilitar a funcionalidade da ferramenta.
  </Step>
</Steps>

Use o `ApifyActorsTool` manualmente para executar o [RAG Web Browser Actor](https://apify.com/apify/rag-web-browser) e realizar uma busca na web:

```python  theme={null}
from crewai_tools import ApifyActorsTool

---

## Inicialize a ferramenta com sua chave de API

**URL:** llms-txt#inicialize-a-ferramenta-com-sua-chave-de-api

linkup_ferramenta = LinkupSearchTool(api_key=os.getenv("LINKUP_API_KEY"))

---

## `SingleStoreSearchTool`

**URL:** llms-txt#`singlestoresearchtool`

**Contents:**
- Description
- Installation
- Environment Variables
- Example

Execute read‑only queries (`SELECT`/`SHOW`) against SingleStore with connection pooling and input validation.

## Environment Variables

Variables like `SINGLESTOREDB_HOST`, `SINGLESTOREDB_USER`, `SINGLESTOREDB_PASSWORD`, etc., can be used, or `SINGLESTOREDB_URL` as a single DSN.

Generate the API key from the SingleStore dashboard, [docs here](https://docs.singlestore.com/cloud/reference/management-api/#generate-an-api-key).

**Examples:**

Example 1 (unknown):
```unknown
## Environment Variables

Variables like `SINGLESTOREDB_HOST`, `SINGLESTOREDB_USER`, `SINGLESTOREDB_PASSWORD`, etc., can be used, or `SINGLESTOREDB_URL` as a single DSN.

Generate the API key from the SingleStore dashboard, [docs here](https://docs.singlestore.com/cloud/reference/management-api/#generate-an-api-key).

## Example
```

---

## Add your provider's API key here too.

**URL:** llms-txt#add-your-provider's-api-key-here-too.

**Contents:**
- 8단계: 필수 종속성 설치
- 9단계: Crew 실행하기
- 10단계: 결과물 검토
- 기타 CLI 명령어 탐색

bash  theme={null}
crewai install
bash  theme={null}
crewai run
bash  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
선택한 provider를 구성하는 방법에 대한 자세한 내용은 [LLM 설정 가이드](/ko/concepts/llms#setting-up-your-llm)를 참고하세요. Serper API 키는 [Serper.dev](https://serper.dev/)에서 받을 수 있습니다.

## 8단계: 필수 종속성 설치

CrewAI CLI를 사용하여 필요한 종속성을 설치하세요:
```

Example 2 (unknown):
```unknown
이 명령어는 다음을 수행합니다:

1. 프로젝트 구성에서 종속성을 읽어옵니다
2. 필요하다면 가상 환경을 생성합니다
3. 모든 필수 패키지를 설치합니다

## 9단계: Crew 실행하기

이제 흥미로운 순간입니다 - crew를 실행하여 AI 협업이 어떻게 이루어지는지 직접 확인해보세요!
```

Example 3 (unknown):
```unknown
이 명령어를 실행하면 crew가 즉시 작동하는 모습을 볼 수 있습니다. researcher는 지정된 주제에 대한 정보를 수집하고, analyst가 그 연구를 바탕으로 종합 보고서를 작성합니다. 에이전트들의 사고 과정, 행동, 결과물이 실시간으로 표시되며 서로 협력하여 작업을 완수하는 모습을 확인할 수 있습니다.

## 10단계: 결과물 검토

crew가 작업을 완료하면, 최종 보고서는 `output/report.md` 파일에서 확인할 수 있습니다. 보고서에는 다음과 같은 내용이 포함됩니다:

1. 요약 보고서
2. 주제에 대한 상세 정보
3. 분석 및 인사이트
4. 권장사항 또는 향후 고려사항

지금까지 달성한 것을 잠시 돌아보세요. 여러분은 여러 AI 에이전트가 협업하여 각자의 전문적인 기술을 발휘함으로써, 단일 에이전트가 혼자서 이루어낼 수 있는 것보다 더 뛰어난 결과를 만들어내는 시스템을 구축한 것입니다.

## 기타 CLI 명령어 탐색

CrewAI는 crew 작업을 위한 몇 가지 유용한 CLI 명령어를 추가로 제공합니다:
```

---

## Zapier Actions Tool

**URL:** llms-txt#zapier-actions-tool

Source: https://docs.crewai.com/pt-BR/tools/automation/zapieractionstool

The `ZapierActionsAdapter` exposes Zapier actions as CrewAI tools for automation.

---

## Store API keys in environment variables

**URL:** llms-txt#store-api-keys-in-environment-variables

**Contents:**
  - 3. Plan for Server Failures

exa_key = os.getenv("EXA_API_KEY")
exa_profile = os.getenv("EXA_PROFILE")

agent = Agent(
    role="Secure Agent",
    goal="Use MCP tools securely",
    backstory="Security-conscious agent",
    mcps=[f"https://mcp.exa.ai/mcp?api_key={exa_key}&profile={exa_profile}"]
)
python  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
### 3. Plan for Server Failures
```

---

## Set up your SERPER_API_KEY key in an .env file, eg:

**URL:** llms-txt#set-up-your-serper_api_key-key-in-an-.env-file,-eg:

---

## SerpApi 구글 쇼핑 도구

**URL:** llms-txt#serpapi-구글-쇼핑-도구

Source: https://docs.crewai.com/ko/tools/search-research/serpapi-googleshoppingtool

SerpApiGoogleShoppingTool은 SerpApi를 사용하여 구글 쇼핑 결과를 검색합니다.

---

## Verify API keys and credentials

**URL:** llms-txt#verify-api-keys-and-credentials

---

## Initialize the tool with an Apify Actor

**URL:** llms-txt#initialize-the-tool-with-an-apify-actor

tool = ApifyActorsTool(actor_name="apify/rag-web-browser")

---

## API 키 설정

**URL:** llms-txt#api-키-설정

os.environ["SERPER_API_KEY"] = "Your Key" # serper.dev API 키
os.environ["OPENAI_API_KEY"] = "Your Key"

---

## Initialize the tool with the Browserbase API key and Project ID

**URL:** llms-txt#initialize-the-tool-with-the-browserbase-api-key-and-project-id

**Contents:**
- 인수

tool = BrowserbaseLoadTool()
```

다음 매개변수를 사용하여 `BrowserbaseLoadTool`의 동작을 맞춤 설정할 수 있습니다:

| 인수                | 타입       | 설명                                                                    |
| :---------------- | :------- | :-------------------------------------------------------------------- |
| **api\_key**      | `string` | *선택 사항*. Browserbase API 키. 기본값은 `BROWSERBASE_API_KEY` 환경 변수입니다.      |
| **project\_id**   | `string` | *선택 사항*. Browserbase 프로젝트 ID. 기본값은 `BROWSERBASE_PROJECT_ID` 환경 변수입니다. |
| **text\_content** | `bool`   | *선택 사항*. 텍스트 콘텐츠만 가져옵니다. 기본값은 `False`입니다.                             |
| **session\_id**   | `string` | *선택 사항*. 기존 세션 ID를 제공합니다.                                             |
| **proxy**         | `bool`   | *선택 사항*. 프록시 활성화/비활성화 옵션입니다. 기본값은 `False`입니다.                         |

---

## Chaves API adicionais (opcional)

**URL:** llms-txt#chaves-api-adicionais-(opcional)

**Contents:**
  - Implementação Completa
  - Executando o Exemplo
- Visualizando Traces no LangDB
  - O Que Você Verá
- Solução de Problemas
  - Problemas Comuns
- Recursos
- Próximos Passos

export SERPER_API_KEY="<sua_chave_api_serper>"  # Para capacidades de busca na web
python  theme={null}
#!/usr/bin/env python3

import os
import sys
from pylangdb.crewai import init
init()  # Inicializar LangDB antes de qualquer importação CrewAI
from dotenv import load_dotenv
from crewai import Agent, Task, Crew, Process, LLM
from crewai_tools import SerperDevTool

def create_llm(model):
    return LLM(
        model=model,
        api_key=os.environ.get("LANGDB_API_KEY"),
        base_url=os.environ.get("LANGDB_API_BASE_URL"),
        extra_headers={"x-project-id": os.environ.get("LANGDB_PROJECT_ID")}
    )

class ResearchPlanningCrew:
    def researcher(self) -> Agent:
        return Agent(
            role="Especialista em Pesquisa",
            goal="Pesquisar tópicos minuciosamente e compilar informações abrangentes",
            backstory="Pesquisador especialista com habilidades em encontrar e analisar informações de várias fontes",
            tools=[SerperDevTool()],
            llm=create_llm("openai/gpt-4o"),
            verbose=True
        )
    
    def planner(self) -> Agent:
        return Agent(
            role="Planejador Estratégico",
            goal="Criar planos acionáveis baseados em descobertas de pesquisa",
            backstory="Planejador estratégico que divide desafios complexos em planos executáveis",
            reasoning=True,
            max_reasoning_attempts=3,
            llm=create_llm("openai/anthropic/claude-3.7-sonnet"),
            verbose=True
        )
    
    def research_task(self) -> Task:
        return Task(
            description="Pesquise o tópico minuciosamente e compile informações abrangentes",
            agent=self.researcher(),
            expected_output="Relatório de pesquisa abrangente com principais descobertas e insights"
        )
    
    def planning_task(self) -> Task:
        return Task(
            description="Crie um plano estratégico baseado nas descobertas da pesquisa",
            agent=self.planner(),
            expected_output="Plano de execução estratégica com fases, objetivos e etapas acionáveis",
            context=[self.research_task()]
        )
    
    def crew(self) -> Crew:
        return Crew(
            agents=[self.researcher(), self.planner()],
            tasks=[self.research_task(), self.planning_task()],
            verbose=True,
            process=Process.sequential
        )

def main():
        topic = sys.argv[1] if len(sys.argv) > 1 else "Inteligência Artificial na Saúde"
        
        crew_instance = ResearchPlanningCrew()
        
        # Atualizar descrições de tarefas com o tópico específico
        crew_instance.research_task().description = f"Pesquise {topic} minuciosamente e compile informações abrangentes"
    crew_instance.planning_task().description = f"Crie um plano estratégico para {topic} baseado nas descobertas da pesquisa"
    
    result = crew_instance.crew().kickoff()
    print(result)

if __name__ == "__main__":
    main()
bash  theme={null}
python main.py "Soluções de Energia Sustentável"
```

## Visualizando Traces no LangDB

Após executar sua aplicação CrewAI, você pode visualizar traces detalhados no dashboard LangDB:

<Frame caption="Dashboard de Trace LangDB">
  <img src="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=74a88afefce3f84fb6f9482a1790b413" alt="Dashboard de trace LangDB mostrando fluxo de trabalho CrewAI" data-og-width="1627" width="1627" data-og-height="890" height="890" data-path="images/langdb-2.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=280&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=8e43fd482dc80800788d7092a8e51f1c 280w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=560&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=02e4ddf9b1499b19d1e221628f5c21a4 560w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=840&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=31e9c94a264d2b33fc9bfbb6a744dc15 840w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=1100&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=5de66fecea56248c974a91c918135e52 1100w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=1650&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=e03d206dd7c466cc5b9de55bab46daf1 1650w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=2500&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=4c16c2587ec6b48bf8cff71b9df17d07 2500w" />
</Frame>

* **Interações de Agentes**: Fluxo completo de conversas de agentes e transferências de tarefas
* **Uso de Ferramentas**: Quais ferramentas foram chamadas, suas entradas e saídas
* **Chamadas de Modelo**: Interações LLM detalhadas com prompts e respostas
* **Métricas de Performance**: Rastreamento de latência, uso de tokens e custos
* **Linha do Tempo de Execução**: Visualização passo a passo de todo o fluxo de trabalho

## Solução de Problemas

* **Nenhum trace aparecendo**: Certifique-se de que `init()` seja chamado antes de qualquer importação CrewAI
* **Erros de autenticação**: Verifique sua chave API LangDB e ID do projeto

<CardGroup cols={3}>
  <Card title="Documentação LangDB" icon="book" href="https://docs.langdb.ai">
    Documentação oficial e guias LangDB
  </Card>

<Card title="Guias LangDB" icon="graduation-cap" href="https://docs.langdb.ai/guides">
    Tutoriais passo a passo para construir agentes de IA
  </Card>

<Card title="Exemplos GitHub" icon="github" href="https://github.com/langdb/langdb-samples/tree/main/examples/crewai">
    Exemplos completos de integração CrewAI
  </Card>

<Card title="Dashboard LangDB" icon="chart-line" href="https://app.langdb.ai">
    Acesse seus traces e análises
  </Card>

<Card title="Catálogo de Modelos" icon="list" href="https://app.langdb.ai/models">
    Navegue por mais de 350 modelos de linguagem disponíveis
  </Card>

<Card title="Recursos Enterprise" icon="building" href="https://docs.langdb.ai/enterprise">
    Opções auto-hospedadas e capacidades empresariais
  </Card>
</CardGroup>

Este guia cobriu o básico da integração do LangDB AI Gateway com CrewAI. Para aprimorar ainda mais seus fluxos de trabalho de IA, explore:

* **Modelos Virtuais**: Crie configurações de modelo personalizadas com estratégias de roteamento
* **Guardrails e Segurança**: Implemente filtragem de conteúdo e controles de conformidade
* **Implantação em Produção**: Configure fallbacks, tentativas e balanceamento de carga

Para recursos mais avançados e casos de uso, visite a [Documentação LangDB](https://docs.langdb.ai) ou explore o [Catálogo de Modelos](https://app.langdb.ai/models) para descobrir todos os modelos disponíveis.

**Examples:**

Example 1 (unknown):
```unknown
### Implementação Completa
```

Example 2 (unknown):
```unknown
### Executando o Exemplo
```

---

## os.environ["TAVILY_API_KEY"] = "YOUR_TAVILY_API_KEY"

**URL:** llms-txt#os.environ["tavily_api_key"]-=-"your_tavily_api_key"

---

## Set up API keys

**URL:** llms-txt#set-up-api-keys

os.environ["SERPER_API_KEY"] = "Your Key" # serper.dev API key
os.environ["OPENAI_API_KEY"] = "Your Key"

---

## Get API keys for services

**URL:** llms-txt#get-api-keys-for-services

OPENAI_API_KEY = getpass("🔑 Enter your OpenAI API key: ")
SERPER_API_KEY = getpass("🔑 Enter your Serper API key: ")

---

## 서비스용 API 키 가져오기

**URL:** llms-txt#서비스용-api-키-가져오기

OPENAI_API_KEY = getpass("🔑 OpenAI API 키를 입력하세요: ")

---

## url="https://web-scraping.dev/products"

**URL:** llms-txt#url="https://web-scraping.dev/products"

---

## 환경 변수에 API 키 저장

**URL:** llms-txt#환경-변수에-api-키-저장

**Contents:**
  - 3. 서버 장애 계획

exa_key = os.getenv("EXA_API_KEY")
exa_profile = os.getenv("EXA_PROFILE")

agent = Agent(
    role="안전한 에이전트",
    goal="MCP 도구를 안전하게 사용",
    backstory="보안을 고려하는 에이전트",
    mcps=[f"https://mcp.exa.ai/mcp?api_key={exa_key}&profile={exa_profile}"]
)
python  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
### 3. 서버 장애 계획
```

---

## SerpApi Google Search Tool

**URL:** llms-txt#serpapi-google-search-tool

Source: https://docs.crewai.com/pt-BR/tools/search-research/serpapi-googlesearchtool

The `SerpApiGoogleSearchTool` performs Google searches using the SerpApi service.

---
