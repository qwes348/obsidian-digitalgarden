---
{"dg-publish":true,"permalink":"/Nfinity7/코이네코/iOS + 구글Ads 전환(이벤트) 보내는법 탐색/","noteIcon":"emoji//1f34e"}
---

----

[[GA4] 앱 전환의 기여도를 계산하는 방법](https://support.google.com/analytics/answer/10311900?hl=en&dark=1&sjid=16085125516051831700-AP)
위 문서를 보면 `Xcode`에서 `AdServices`프레임워크를 추가해야 한다는 언급이 있음.

~~하지만 당연히
그냥 추가만 하면 안될것 같고...
Unity와 어떻게 통합하는지 찾아봐야함~~
↳ [이 에셋](https://assetstore.unity.com/packages/tools/utilities/egoxproject-ios-tvos-xcode-project-and-info-plist-editor-21661?locale=ko-KR)을 사용하면 쉽게 추가할 수 있다.
- [다음 라이브러리/프레임워크를 Unity XCode 프로젝트에 연결합니다.](https://support.singular.net/hc/ko/articles/360037635452--UPDATED-Unity-SDK-%EC%97%B0%EB%8F%99-%EA%B0%80%EC%9D%B4%EB%93%9C)
	- Security.framework
	- SystemConfiguration.framework
	- iAD.framework
	- AdSupport.framework
	- WebKit.framework
	- libsqlite3.0.tbd
	- libz.tbd
	- StoreKit.framework
	- AdServices.framework (**반드시 추가되어야 하나**, 이는 iOS 14.3 이상의 디바이스에서만 제공되므로 **선택사항**입니다)

[iAd와 AdServices: 차이점은 무엇입니까?](https://www.revenuecat.com/blog/engineering/iad-vs-adservices-whats-the-difference/)
`iOS 14.3` 이후로 `iAd`프레임워크가 `AdServices`프레임워크로 바뀐것 같음
현재 우리 Unity에서는 iOS용 `.dll` 아무거나에 의존성을 추가할려고 보면
iAd가 있음 흠....

[유니티에서 커스텀 이벤트 로깅 가이드 문서](https://firebase.google.com/docs/analytics/unity/events?hl=ko#ios+)
[GA4 추천 이벤트 목록](https://support.google.com/analytics/answer/9267735?visit_id=638297345298713762-1434892157&rd=1)
이걸로 커스텀 이벤트를 iOS전용으로 만들고 로그를 남겨도 되긴 될것같다만...
그럼 기본 이벤트들은 왜 iOS는 Ads에서 안뜰까??
↳ 일단 이거는 말그대로 이벤트 로깅이고 진짜 찾아야 하는것은 광고를 보고 설치했다는 "전환"이다.

[광고주를 위한 iOS14 가이드라인 (유니티)](https://docs.unity.com/acquire/en-us/manual/iOS-14-guidelines)
이 가이드를 보면 `SKAdNetwork`가 핵심인것 같다.
그렇다면 `SKAdNetwork`를 어떻게 유니티에 통합하는가?
[Unity iOS14 Advertistion Support 패키지](https://docs.unity3d.com/Packages/com.unity.ads.ios-support@1.2/manual/index.html)
[매뉴얼](https://docs.unity.com/ads/en-us/manual/InstallingTheiOS14SupportPackage)
이 패키지 문서를 보면,
`SkAdNetworkRegisterAppForNetworkAttribution()` 이 함수 호출으로
`SKAdNetwork`에 등록? 할 수 있다고 한다.

추가로,
위 패키지의 기능으로 광고 추적 허용 팝업을 띄울수 있다고 한다.
[방법1](https://boxwitch.tistory.com/entry/%EC%9C%A0%EB%8B%88%ED%8B%B0-iOS-IDFA-%EA%B4%91%EA%B3%A0%EC%B6%94%EC%A0%81-%ED%97%88%EC%9A%A9-%ED%8C%9D%EC%97%85)
[방법2](https://hkn10004.tistory.com/90)
필수인지는 모르겠으나 해두는게 좋을것 같다.
그리고 `Info.plist`에 아래 코드를 추가하자
```XML
<key>NSUserTrackingUsageDescription</key>
<string>Your data will be used to measure advertising efficiency.</string>
```
        


[SKAdNetwork 공식문서](https://developer.apple.com/documentation/storekit/skadnetwork)
![](https://i.imgur.com/PSqTJu2.png)

[광고 네트워크 ID구성](https://docs.unity.com/ads/en-us/manual/ConfiguringAdNetworkIDs)
이런 문서를 보면 `Info.plist`에 막 머를 적어야된다고 하는데
Unity광고 패키지를 쓰면 자동으로 된다~ 머 이렇게 적혀있다
근데 코이네코 프로젝트는 어떤 패키지가 해주는지는 모르겠지만
빌드하고 Xcode에서 확인해보면 `SKAdNetworkItems` 배열이 Info에 추가돼있다.
**따라서** 위 문서는 안따라해도 될것같다.

**여기서 남은 문제는 구글Ads에 iOS설치 전환추적을 "어떻게" 연결하는가?**


[유료 솔루션인데 SKAdNetwork설명해주는 문서](https://help.dfinery.io/hc/ko/articles/6472668522265-SkAdNetwork-SKAN-Conversion-Value-%EC%86%94%EB%A3%A8%EC%85%98-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
[위랑 같은 유료솔루션의 SKAdNetwork 캠페인 활용하기 문서](https://help.dfinery.io/hc/ko/articles/6474611664281-SKAdNetwork-SKAN-%EC%BA%A0%ED%8E%98%EC%9D%B8-%ED%99%9C%EC%9A%A9%ED%95%98%EA%B8%B0)