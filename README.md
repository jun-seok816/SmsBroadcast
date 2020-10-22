# initializeWebView메소드

## Description 

- 자바스크립트에서 안드로이드 메소드를 인식할 수 있게 설정하는 메소드.
- 제공된 이름을 사용하여 자바스크립트에서 안드로이드 메소드에 엑세스 할 수 있습니다.
            
## Parameter

- 없음
    
## Return
- type : void

- value : 없음

## Dependence function

- getSettings()
  - WebView의 설정을 제어하는데 필요한 WebSettings 객체를 가져옵니다.
  - https://developer.android.com/reference/android/webkit/WebView#getSettings()

- addJavascriptInterface: 
  - 제공된 java객체를 webView에 삽입합니다. 
  - https://developer.android.com/reference/android/webkit/WebView

- setClickable(): 
  - 버튼을 활성화/비활성화시킬 수 있다

- setJavaScriptEnabled(true or falee): 
  - WebView에서 JavaScript실행을 사용하도록 지시합니다
  - https://developer.android.com/reference/android/webkit/WebSettings#setJavaScriptEnabled(boolean)
  
- setJavaScriptCanOpenWindowsAutomatically(true or false): 
  - 자동으로 창을 열도록 JavaScript에 지시합니다.
  - https://developer.android.com/reference/android/webkit/WebSettings#setJavaScriptCanOpenWindowsAutomatically(boolean)

- setAllowUniversalAccessFromFileURLs(true or false):
  - 파일 체계 URL의 Context에서 원본 간 요청이 다른 파일 체계 URL의 콘텐츠에 액세스 할 수 있도록 허용할지 여부를 설정합니다.
  - https://developer.android.com/reference/android/webkit/WebSettings#setAllowUniversalAccessFromFileURLs(boolean)

- setAllowFileAccessFromFileURLs(true or false): 
  - 파일 체계 URL의 Context에서 실행되는 Javascript가 모든 출처의 콘텐츠에 엑세스 할 수 있는지의 여부
  - https://developer.android.com/reference/android/webkit/WebSettings#setAllowFileAccessFromFileURLs(boolean)
  
- setBuiltInZoomControls(true or false): 
  - WebView가 내장 된 확대 / 축소 메커니즘을 사용해야하는지 여부를 설정합니다.
  - https://developer.android.com/reference/android/webkit/WebSettings#setBuiltInZoomControls(boolean)
  
- setSupportZoom(true or false): 
  - WebView가 화면 확대 / 축소 컨트롤 및 제스처를 사용하여 확대 / 축소를 지원해야하는지 여부를 설정합니다.
  - https://developer.android.com/reference/android/webkit/WebSettings#setSupportZoom(boolean)
  
- setLightTouchEnabled(true or false): 
  - 가벼운 터치를 사용하여 선택하고 마우스 오버를 활성화 할 수 있습니다.
  - https://developer.android.com/reference/android/webkit/WebSettings#setLightTouchEnabled(boolean)
  
- setDomStorageEnabled(true or false): 
  - DOM 저장소 API 사용 여부를 설정합니다.
  - https://developer.android.com/reference/android/webkit/WebSettings#setDomStorageEnabled(boolean)
  
- setPluginState(WebSettings.PluginState state): 
  - WebView에 요청시 플러그인을 활성화, 비활성화 또는 포함하도록 지시합니다
  - https://developer.android.com/reference/android/webkit/WebSettings#setPluginState(android.webkit.WebSettings.PluginState)
  
- setLoadWithOverviewMode(true or false):
  - WebView가 개요 모드에서 페이지를로드할지 여부를 설정합니다.즉, 콘텐츠를 너비별로 화면에 맞게 축소합니다.
  - https://developer.android.com/reference/android/webkit/WebSettings#setLoadWithOverviewMode(boolean)'
  
- setUseWideViewPort(true or false):
  - WebView가 "viewport"HTML 메타 태그에 대한 지원을 활성화해야하는지 아니면 와이드 뷰포트를 사용해야하는지 여부를 설정합니다.
  - https://developer.android.com/reference/android/webkit/WebSettings#setUseWideViewPort(boolean)
  
- setRenderPriority( WebSettings.RenderPriority): 
  - 렌더 스레드의 우선 순위를 설정합니다.
  - https://developer.android.com/reference/android/webkit/WebSettings#setRenderPriority(android.webkit.WebSettings.RenderPriority)
  
- setCacheMode(int mode): 
  - 캐시가 사용되는 방식을 재정의합니다. 
  - https://developer.android.com/reference/android/webkit/WebSettings#setPluginState(android.webkit.WebSettings.PluginState)


- setWebViewClient(): 
  - 다양한 알림과 요청을받을 WebViewClient를 설정합니다. 
  - https://developer.android.com/reference/android/webkit/WebView#setWebViewClient(android.webkit.WebViewClient)
  
- onPageStarted(): 
  - WebView에서 처음 한 번만 호출되는 메소드, 페이지 로딩이 시작된 것을 알립니다. 
  - https://developer.android.com/reference/android/webkit/WebViewClient#onPageStarted(android.webkit.WebView,%20java.lang.String,%20android.graphics.Bitmap)
  
- onPageFinished():
  - WebView에서 처음 한 번만 호출되는 메소드, 페이지 로딩이 완료된 것을 알립니다.
  - https://developer.android.com/reference/android/webkit/WebViewClient#onPageFinished(android.webkit.WebView,%20java.lang.String)
  
- shouldOverrideUrlLoading(): 
  - 새로운 URL이 현재 WebView에 로드되려고 할 때 호스트 응용 프로그램에게 컨트롤을 대신할 기회를 줍니다
  - https://developer.android.com/reference/android/webkit/WebViewClient#shouldOverrideUrlLoading(android.webkit.WebView,%20android.webkit.WebResourceRequest)
  
- onReceivedSslError():
  - SSL 오류를 무시할 때 쓰는 코드>https://aorica.tistory.com/103
  - https://developer.android.com/reference/android/webkit/WebViewClient#onReceivedSslError(android.webkit.WebView,%20android.webkit.SslErrorHandler,%20android.net.http.SslError)
  
- onReceivedError(): 
  - 호스트 응용 프로그램에게 오류를 보고합니다.
  - https://developer.android.com/reference/android/webkit/WebViewClient#onReceivedError(android.webkit.WebView,%20int,%20java.lang.String,%20java.lang.String)
  - http://ankyu.entersoft.kr/lecture/android/webview_02.asp
## Source code    
    
    ```
    @SuppressLint("JavascriptInterface")
    public void initializeWebView() {
        WebSettings webSettings = wv.getSettings();

        wv.addJavascriptInterface(new WebVCamBridgeInterface(), "AndroidDevice");
        wv.setClickable(true);
        webSettings.setJavaScriptEnabled(true);
        webSettings.setJavaScriptCanOpenWindowsAutomatically(true);
        webSettings.setAllowFileAccessFromFileURLs(true);
        webSettings.setAllowUniversalAccessFromFileURLs(true);
        webSettings.setBuiltInZoomControls(true);
        webSettings.setSupportZoom(true);
        webSettings.setLightTouchEnabled(true);
        webSettings.setDomStorageEnabled(true);
        webSettings.setPluginState(WebSettings.PluginState.ON);


        webSettings.setLoadWithOverviewMode(false);
        webSettings.setUseWideViewPort(false);


        webSettings.setRenderPriority(WebSettings.RenderPriority.HIGH);
        webSettings.setCacheMode(WebSettings.LOAD_NO_CACHE);

        wv.setWebViewClient(new WebViewClient() {
            @Override
            public void onPageStarted(WebView view, String url, Bitmap favicon) {
                super.onPageStarted(view, url, favicon);
            }

            @Override
            public void onPageFinished(WebView view, String url) {
                super.onPageFinished(view, url);

            }

            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                return super.shouldOverrideUrlLoading(view, url);
            }

            @Override
            public void onReceivedSslError(WebView view, SslErrorHandler handler, SslError error) {
                handler.proceed();
            }

            @Override
            public void onReceivedError(WebView view, int errorCode, String description, String failingUrl) {
                super.onReceivedError(view, errorCode, description, failingUrl);
            }

        });
    }
    ```
    
# ShowSMS2()메소드
## Description 

- 자바스크립트에서 실행시키는 안드로이드함수

## Parameter

- 없음

## Return
- type : void

- value : 없음

```
 @JavascriptInterface
    public void ShowSMS2 () {
        sendSMS("01039750810", "4567");
        }
```
    
# SMS()메소드

## Description 

- 안드로이드에서 실행시키는 자바스크립트함수

## Parameter

- 없음
    
## Return
- type : void

- value : 없음

## Dependence function

- load.url(): 안드로이드에서 SMS메소드가 실행되면wv.loadurl("javascript:(function(){}문구가 안에 있는 Javascript 코드를 실행시킨다.

## Source code

```
public void SMS(){

        a = "전화번호" +tv_sender + "인증번호" + tv_content;
        wv.post(new Runnable() {
            @Override
            public void run() {
                    wv.loadUrl("javascript:(function() { "
                            + "document.getElementById('aa').innerHTML = '"+a+"'; "
                            + "})()");
            }
        });
    }
```
    

# Javascript코드    

## Description 

- 자바스크립트에서 안드로이드 메소드를 호출
            

## Dependence function

- ShowSMS2():SendSms메소드 호출
  - https://github.com/jun-seok816/junseok-android

## Source code 

```
var e = document.getElementById('aa');
       var c=AndroidDevice.ShowSMS2();
       e.innerHTML=c;
    AndroidDevice.ShowSMS2 ();
    
```


## Further explanation

- addJavascriptInterface 메소드를 webview에 삽입된 자바객체에서 안드로이드 메소드를 호출하는 모습
  - AndroidDevice.ShowSMS2();
- 이때 호출되는 안드로이드 메소드에는 @JavascriptInterface객체가 달려있어야 호출 할 수 있다.
- 반대로 안드로이드에서 자바스크립트 함수를 호출시키기 위해서는 WebView와 Android는 비동기 상태 이므로 쓰레드로 넣어 전달해 주어야 한다.
  - https://developer.android.com/reference/java/lang/Thread
  - https://nicgoon.tistory.com/192



    
