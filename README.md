GIF、JPEG、JPG、MOV、MP4、PNG、SVG或WEBM预演
此文件为空。缩进模式
GIF、JPEG、JPG、MOV、MP4、PNG、SVG或 WEBM
此文件为空。缩进模式
再试一次空
使用一个不空的文件。制表符
这个文件是隐藏的。缩进尺寸

on:
  workflow_dispatch:
  push:
    branches:
再试一次换行模式
  schedule:
另一份文件。无包裹

jobs:
  build:
另一份文件。无包裹
    
query为空
query为空
 
query为空
query为空
      with:
        fetch-depth: 0
 
    - name: Make changes
      run: |
        echo "Some changes" >> changes.txt
        date > time
        date
        echo 1 > 1
 
    - name: Commit changes
      uses: stefanzweifel/git-auto-commit-action@v5
Skip to content
Navigation Menu
Sign in
zjyzip
/
AdClose
Public
Code
Pull requests
Actions
Commit
tweak RequestHook.
 main
@zjyzip
zjyzip authored 2 days ago
1 parent 9845daf
commit 273da7c
Showing 1 changed file with 15 additions and 18 deletions.
  33 changes: 15 additions & 18 deletions33  
app/src/main/java/com/close/hook/ads/hook/gc/network/RequestHook.java
Original file line number	Diff line number	Diff line change
@@ -1,66 +1,59 @@
package com.close.hook.ads.hook.gc.network;
import android.content.ContentResolver;
import android.content.Context;
import android.content.Intent;
import android.database.Cursor;
import android.net.Uri;
import android.util.Log;
import androidx.annotation.Nullable;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.webkit.WebResourceRequest;
import com.close.hook.ads.data.model.BlockedRequest;
import com.close.hook.ads.data.model.RequestDetails;
import com.close.hook.ads.data.model.Url;
import com.close.hook.ads.hook.util.ContextUtil;
import com.close.hook.ads.hook.util.DexKitUtil;
import com.close.hook.ads.hook.util.HookUtil;
import com.close.hook.ads.hook.util.StringFinderKit;
import com.close.hook.ads.provider.UrlContentProvider;
import com.google.common.cache.Cache;
import com.google.common.cache.CacheBuilder;
import org.luckypray.dexkit.result.MethodData;
import java.io.IOException;
import java.lang.reflect.Field;
import java.lang.reflect.Method;
import java.nio.charset.StandardCharsets;
import java.net.InetAddress;
import java.net.MalformedURLException;
import java.net.URL;
import java.net.URLDecoder;
import java.util.List;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.ConcurrentHashMap;
import kotlin.Triple;
import de.robv.android.xposed.XposedBridge;
import de.robv.android.xposed.XposedHelpers;
public class RequestHook {
    private static final String LOG_PREFIX = "[RequestHook] ";
    private static final Object EMPTY_WEB_RESPONSE = createEmptyWebResourceResponse();
    private static final ConcurrentHashMap<String, Boolean> dnsHostCache = new ConcurrentHashMap<>();
    private static final ConcurrentHashMap<String, Boolean> urlStringCache = new ConcurrentHashMap<>();

    private static Context applicationContext;

    static {
        ContextUtil.addOnApplicationContextInitializedCallback(() -> {
            applicationContext = ContextUtil.applicationContext;
            initHooks();
        });
    }

    private static final Uri CONTENT_URI = new Uri.Builder()
        .scheme("content")
        .authority(UrlContentProvider.AUTHORITY)
@@ -73,21 +66,25 @@ public class RequestHook {
        .concurrencyLevel(Runtime.getRuntime().availableProcessors() * 2)
        .build();

    private static void initHooks() {
    public static void init() {
        try {
            setupDNSRequestHook();
            setupHttpRequestHook();
            setupOkHttpRequestHook();
            setWebViewRequestHook();
            ContextUtil.addOnApplicationContextInitializedCallback(() -> {
                applicationContext = ContextUtil.applicationContext;

                try {
                    setupDNSRequestHook();
                    setupHttpRequestHook();
                    setupOkHttpRequestHook();
                    setupWebViewRequestHook();
                } catch (Exception e) {
                    XposedBridge.log(LOG_PREFIX + "Error while hooking: " + e.getMessage());
                }
            });
        } catch (Exception e) {
            XposedBridge.log(LOG_PREFIX + "Error while hooking: " + e.getMessage());
            XposedBridge.log(LOG_PREFIX + "Error during initialization: " + e.getMessage());
        }
    }

    public static void init() {
        initHooks();
    }

    private static String calculateCidrNotation(InetAddress inetAddress) {
        byte[] addressBytes = inetAddress.getAddress();
        int prefixLength = 0;
@@ -383,7 +380,7 @@ private static boolean processHttpRequest(Object request, Object response, URL u
        }
    }

    public static void setWebViewRequestHook() {
    public static void setupWebViewRequestHook() {
        try {
            HookUtil.findAndHookMethod(
                WebView.class,
0 comments on commit 273da7c
Please sign in to comment.
Footer
© 2025 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact
Manage cookies
Do not share my personal information
