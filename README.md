# Battle.net-Funcaptcha
A simple trick to get the best captchas when loading their webpage on a proxy

Video Demo: https://www.youtube.com/watch?v=8ESSx5QqLBY

As you can see in the video, im able to "generate" a bunch of captcha tokens to use later on, all without a captcha service.

Releasing this because I am the creator of it :)

What this allows you to do:
  
   Let's you load the best possible captcha after loading up blizzard sign up page with a proxy.
   This is simply a trick and not really a "bypass".
   
I simply found this trick by loading up the blizzard webpage on a proxy, then disabling the proxy before loading the captcha, and low and behold I got the best captcha as it was loading up on my home IP, which is clean. This allows you to load the web page up as many times as you want (as long as you have proxies) and will let you get 0 click captchas if done right (you will get 1-2 click captchas at times, after solving a few it goes back to 0 click captchas)

Steps to replicate this (without code)

1. Start up firefox and set an HTTP proxy.
2. Go to the blizzard sign up page
3. Before clicking "Continue" to load up the captcha, disable the proxy.
4. Click "Continue" and you should get an easy captcha (if any)

How to do it with selenium:

You will need selenium wire and firefox to do this!

Setup your selenium like normal, but intercept the requests with this:
```
browser.request_interceptor = interceptor
```

This will capture all request, headers, etc. Now for the interceptor function:
```
def interceptor(request):
    if(request.url == "https://account.battle.net/creation/flow/creation-full/step/get-started"):
        response = request.body.decode('utf-8')
        splitted = response.split('name="arkose"\r\n\r\n')
        token = splitted[1].split('|')
        print(token[0])
        request.abort()
```   
     
This will intercept the request just before the country, dob, and funcaptcha token gets sent to blizzard. This will block the request and get the captcha token so that you can use it on another session (For example a session with proxies)

As long as you dont submit a captcha, you will constantly get 0 click captchas (until you need to solve a few 1-2 click captchas). This is how I achieved the "Captcha Bypass" in Hexogen.

#Never share code or ideas with even those you think you trust.









  
 
