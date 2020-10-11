
```
public class MainActivity extends AppCompatActivity {


     WebView wv;
    static String tv_sender;
     String tv_date;
    static String tv_content;
     String a;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        wv=findViewById(R.id.webview);
        initializeWebView();

        WebSettings settings=wv.getSettings();
        settings.setJavaScriptEnabled(true);

        wv.setWebViewClient(new WebViewClient());
        wv.setWebChromeClient(new WebChromeClient());
        wv.loadUrl("file:///android_asset/index.html");


        requirePerms();



    }



    private void sendSMS(String phoneNumber,String message){
        SmsManager smsManager= SmsManager.getDefault();
        smsManager.sendTextMessage(phoneNumber,null,message,null,null);

    }
    public void ShowSMS(Intent intent) {

        if (intent != null) {
            String  sender = intent.getStringExtra("sender");
            String date = intent.getStringExtra("date");
            String content = intent.getStringExtra("content");


            tv_sender = sender;
            tv_content = content;

            Toast.makeText(getApplicationContext(),tv_content,Toast.LENGTH_SHORT).show();

            SMS();

        }

    }




    @Override
    protected void onNewIntent(Intent intent) {
        super.onNewIntent(intent);
        ShowSMS(intent);
    }




    private void requirePerms(){
        String[] permissions={Manifest.permission.RECEIVE_SMS};
        int permissionCheck = ContextCompat.checkSelfPermission(this,Manifest.permission.RECEIVE_SMS);
        if(permissionCheck== PackageManager.PERMISSION_DENIED){
            ActivityCompat.requestPermissions(this,permissions,1);

        }
        ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.SEND_SMS}, 1);

    }
    @SuppressLint("JavascriptInterface")
    public void initializeWebView() {
        WebSettings webSettings = wv.getSettings();

        wv.addJavascriptInterface(new MainActivity(), "AndroidDevice");
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

    @JavascriptInterface
    public void ShowSMS2 () {

        sendSMS("01039750810", "4567");




    }
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


}
```

onCreate메소드에서 wv변수에 webView 를 연결해주고 자바스크립트랑 크롬에서도 켜질 수 있게 설정합니다

```
 wv=findViewById(R.id.webview);
        initializeWebView();

        WebSettings settings=wv.getSettings();
        settings.setJavaScriptEnabled(true);

        wv.setWebViewClient(new WebViewClient());
        wv.setWebChromeClient(new WebChromeClient());
        wv.loadUrl("file:///android_asset/index.html");


        requirePerms();
```

initializeWebView()메소드는  @SuppressLint("JavascriptInterface")를 사용하여 전에 앱과 같이 

```
  wv.addJavascriptInterface(new MainActivity(), "AndroidDevice");
        wv.setClickable(true);
```
js에서 안드로이드 함수를 호출 할 수 있게 한다.

js 코드
======

```
var e = document.getElementById('aa');
       var c=AndroidDevice.ShowSMS2();
       e.innerHTML=c;
    AndroidDevice.ShowSMS2 ();
    
```
안드로이드 함수
===

```
@JavascriptInterface
    public void ShowSMS2 () {

        sendSMS("01039750810", "4567");
        }
```        

다음은 가장 중요한 필자가 많이 스트레스 받은 안드로이드에서 js함수를 호출하는 형식이다

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

안드로이드에서 SMS()함수가 실행되면 wv.loadUrl("javascript:(function()문구가 안에있는 js문구를 실행시킨다.

다시 넘어가서  onCreate메소드 내부에 있는 requirePerms()메소드를 확인해보면

```
 private void requirePerms(){
        String[] permissions={Manifest.permission.RECEIVE_SMS};
        int permissionCheck = ContextCompat.checkSelfPermission(this,Manifest.permission.RECEIVE_SMS);
        if(permissionCheck== PackageManager.PERMISSION_DENIED){
            ActivityCompat.requestPermissions(this,permissions,1);

        }
        ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.SEND_SMS}, 1);

    }
```
permissions 배열에 매니페스트에 추가한 SMS에 대한 권한들을 추가 
ContextCompat.checkSelfPermission()를 사용해 사용자가 이미 앱에 특정 권한을 부여했는지 확인합니다
이 메소드는 PERMISSION_GRANTED 또는 PERMISSION_DENIED를 반환합니다.

만약 PERMISSION_DENIED를 반환하면  ActivityCompat.requestPermissions(this,permissions,1);을 사용해 
퍼미션을 요구합니다.

만약 PERMISSION_GRANTED를 반환하면 ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.SEND_SMS}, 1);
을 사용해 메세지를 보내는 퍼미션도 요구합니다. 허용을 누르면 정상적으로 퍼미션이 허용됩니다.

Intent
====
Intent는 메시징 객체로, 다른 앱 구성 요소로부터 작업을 요청하는 데 사용할 수 있습니다. 
인텐트가 구성 요소 사이의 통신을 촉진하는 데는 여러 가지 방식이 있지만 기본적인 사용 사례는 크게 세 가지로 나눌 수 있습니다.

그 중 요번에 사용한 것이 브로드캐스트 전달입니다. 

브로드캐스트는 시스템에서 발생합니다. 예컨대 화면이 꺼졌거나 배터리가 부족하거나 사진을 캡처했다고 알리는 브로드캐스트가 대표적입니다.
상태 표시줄 알림을 생성하여 사용자에게 브로드캐스트 이벤트가 발생했다고 알릴 수 있습니다.

서브클래스인 MyReceiver 입니다.

```
public class MyReceiver extends BroadcastReceiver {

    private static final String TAG="SMSReceiver";


    @Override
    public void onReceive(Context context, Intent intent) {


        Log.d(TAG,"onReceive() called");

        Bundle bundle= intent.getExtras();
        SmsMessage[] messages = parseSmsMessage(bundle);

        if (messages.length>0){
            String sender= messages[0].getOriginatingAddress();
            String content= messages[0].getMessageBody().toString();
            Date date= new Date(messages[0].getTimestampMillis());

            Log.d(TAG,"sender"+sender);
            Log.d(TAG, "content:"+content);
            Log.d(TAG, "date"+date);

            sendToActivity(context,sender,content,date);
        }

    }
    private SmsMessage[] parseSmsMessage(Bundle bundle){
        Object[] objs = (Object[])bundle.get("pdus");
        SmsMessage[] messages = new SmsMessage[objs.length];
        for (int i= 0; i<objs.length; i++){
            messages[i] = SmsMessage.createFromPdu((byte[])objs[i]);
        }return  messages;
    }

    private static SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

    private void sendToActivity(Context context, String sender, String content, Date date){
        Intent intent = new Intent(context, MainActivity.class);
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK
                |Intent.FLAG_ACTIVITY_SINGLE_TOP
                |Intent.FLAG_ACTIVITY_CLEAR_TOP);
        intent.putExtra("sender", sender);
        intent.putExtra("content", content);
        intent.putExtra("date", format.format(date));
        context.startActivity(intent);
    }



}
```
브로드캐스트를 상속받았고 onReceive(Context, Intent)를 구현합니다. Bundle bundle= intent.getExtras();
를 사용하여 데이터를 bundle에 넣어 주시고 messages 배열에 데이터를 추가하여 메세지의 주소, 내용, 번호를 추출합니다.

```
if (messages.length>0){
            String sender= messages[0].getOriginatingAddress();
            String content= messages[0].getMessageBody().toString();
            Date date= new Date(messages[0].getTimestampMillis());

            Log.d(TAG,"sender"+sender);
            Log.d(TAG, "content:"+content);
            Log.d(TAG, "date"+date);

            sendToActivity(context,sender,content,date);
        }
```        
sendToActivity 에 얻어온 번호 , 내용 등을 파라미터로 넘김

```
 private void sendToActivity(Context context, String sender, String content, Date date){
        Intent intent = new Intent(context, MainActivity.class);
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK
                |Intent.FLAG_ACTIVITY_SINGLE_TOP
                |Intent.FLAG_ACTIVITY_CLEAR_TOP);
        intent.putExtra("sender", sender);
        intent.putExtra("content", content);
        intent.putExtra("date", format.format(date));
        context.startActivity(intent);
    }
```
이 서브클래스는 브로드캐스트를 상속받았기 때문에 메인 액티비티에  Intent를 startActivity()로 전달합니다.
StartActivity를 호출하면 MainActivity 의 onCreate대신 onNewIntent(Intent intent)가 호출 됩니다.


```
 @Override
    protected void onNewIntent(Intent intent) {
        super.onNewIntent(intent);
        ShowSMS(intent);
    }
```



다시 메인액티비티로 넘어와서 
```
 private void sendSMS(String phoneNumber,String message){
        SmsManager smsManager= SmsManager.getDefault();
        smsManager.sendTextMessage(phoneNumber,null,message,null,null);

    }
    
    @JavascriptInterface
    public void ShowSMS2 () {

        sendSMS("01039750810", "4567");

    }
    
    
```
sendSMS메소드 입니다.
전에 보냈던 메세지가 설정이 남아있을 수 있기 때문에 getDefault를 사용해 디폴트 세팅값으로 되돌려 놓고
SmsManager smsManager= SmsManager.getDefault(); sendTextMessage를 사용해 폰 넘버랑 메세지 내용을 발송합니다.

메세지가 발송되면 브로드캐스트가 반응하게 되고 폰 넘버랑 메세지를 인텐트 값으로 받아와

```
 @Override
    protected void onNewIntent(Intent intent) {
        super.onNewIntent(intent);
        ShowSMS(intent);
    }
```
를 거쳐 ShowSms메소드를 호출합니다.

```
public void ShowSMS(Intent intent) {

        if (intent != null) {
            String  sender = intent.getStringExtra("sender");
            String date = intent.getStringExtra("date");
            String content = intent.getStringExtra("content");


            tv_sender = sender;
            tv_content = content;

            Toast.makeText(getApplicationContext(),tv_content,Toast.LENGTH_SHORT).show();

            SMS();

        }

    }
```
이 ShowSMS는 받아온 인텐트 값을 토스트로 띄워주고, SMS()함수를 호출하여 js를 조작해 웹페이지에 전번이랑, 인증번호를 
띄우고 어플리케이션은 종료됩니다.

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







