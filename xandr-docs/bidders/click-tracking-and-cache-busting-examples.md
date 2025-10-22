---
title: Click Tracking and Cache-Busting Examples for Top Ad Servers
description: Learn about the appropriate locations in which to insert the click tracking macro in your third-party ad tags in order for Xandr to track clicks properly.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# Click tracking and Cache-Busting examples for top Ad servers

## Macro definitions

**Click tracking**

If you want to track clicks and you are hosting your creatives on one of the ad servers below, this page shows the appropriate locations in which to insert the click tracking macro in your third-party ad tags in order for Xandr to track clicks properly. To locate it in the samples below, search for `CLICK_URL`.

| Macro | Description |
|--|--|
| `${CLICK_URL}` | The click tracking URL. <br> For example:  `https://xandr.com` |
| `${CLICK_URL_ENC}` | The encoded click tracking URL (only necessary for some third-party ad servers). For example:  `https%3A%2F%2Fxandr.com` |

**Cache-busting**

The cache-buster macro ensures that a fresh call is made to the ad server every time the tag is called, so you’re accurately counting impressions. If you don't add the cache-busting macro to the tag, you will be more likely to see impression counting discrepancies. If you want to perform cache-busting and you are hosting your creatives on one of the ad servers below, use the examples on this page to find the appropriate locations in which to insert the cache-busting macro in your third-party ad tags. To locate it in the samples below, search for `CACHEBUSTER`.

> [!NOTE]
> All examples on this page were provided by clients or a third-party server. As a result, Xandr has no control over any changes made by those third-party servers that may cause these macros not to function. If the macro you are using is not working correctly, please contact your third-party server. If the third-party server you use is not listed here, Xandr will be unable to confirm the proper placement of these macros in their tag as the location of the tag in which you place the macro must be provided by your third-party server (Xandr only provides the click URL by filling the macro). For troubleshooting tips, see the [Click Tracking page](../monetize/click-tracking.md) in the UI.

## Ad Server-Specific examples

> [!WARNING]
> The code examples noted below are indicative only and not necessarily up-to-date.

**AdForm**

``` 
<script language="javascript" src="http://track.adform.net/adfscript/?bn=123456;click=${CLICK_URL}"></script>
<noscript>
<a href="${CLICK_URL}http://track.adform.net/C/?bn=123456;C=0" target="_blank">
<img src="media/?bn=123456;srctype=4;ord=${CACHEBUSTER}" border="0" width="930" height="180" alt=""/>
</a>
</noscript>
```

**AdGear**

``` 
<script type="text/javascript" language="JavaScript">
(function() {
ADGEAR_SOURCE_CLICKTRACKER = "${CLICK_URL}";
ADGEAR_SOURCE_CLICKTRACKER_EXPECTS_ENCODED = false;
ADGEAR_SOURCE_CLICKTRACKER_IS_ENCODED = false;
ADGEAR_SOURCE_CLICKTRACKER_IS_DOUBLE_ENCODED = false;
var randomnum = "{CACHEBUSTER}";
var agref = "";
var proto = "http:";
if (!agref.match(/^https?/i)) agref = "";
if (window.location.protocol == "https:") proto = "https:";
if (randomnum.substring(0,2) == "__") randomnum = String(Math.random());
document.writeln('<scr' + 'ipt type="text/ja' + 'vascr' + 'ipt" s' + 'rc="' +
proto + '//d.adgear.com' + '/impressions/ext/p=' +
'1234' + '.js?AG_R=' + randomnum +
(agref === "" ? "" : ("&AG_REF=" + encodeURIComponent(agref))) +
'"></scr' + 'ipt>');
})();
</script>
```

**AdInterax**

``` 
<SCRIPT>adx_U_555555="";adx_D_55555="${CLICK_URL}";adx_I_555555="";</SCRIPT>

<SCRIPT
SRC="http://mi.adinterax.com/js/denvernp,atencio_300X_seren,C=XXXXX,P=XXXXX/ad2.js?q=55555555" LANGUAGE="JavaScript"></SCRIPT>

<NOSCRIPT><A HREF="${CLICK_URL}http://tr.adinterax.com/re/denvernp,atencio_300X_seren,C=XXXXXX ,P=XXXXX/0/0/tc,c:noscript/http://www.johnatencio.com/search?q=new+heart&x=16&y=9"><IMG SRC="http://tr.adinterax.com/re/XXXXXX,atencio_300X_seren,C=John_atencio,
P=Scott/0/0/in,ti/http://mi.adinterax.com/customer/XXXXXXX/0/300x250_FL_newart.jpg?adxq=1282775581" BORDER=0></A></NOSCRIPT>
```

**Adition**

``` 
<!-- BEGIN ADITIONTAG -->
<script type="text/javascript" src="http://imagesrv.adition.com/js/adition.js"></script>
<script type="text/javascript" src="http://ad1.adfarm1.adition.com/js?wp_id=12345&kid=12345&clickurl=${CLICK_URL}"></script>
<noscript><a href="${CLICK_URL}http://ad1.adfarm1.adition.com/click?sid=12345&ts=${CACHEBUSTER}">
<img src="media/banner?sid=12345&kid=12345&ts=${CACHEBUSTER}" border="0"></a></noscript>
<!-- END ADITIONTAG -->
```

**AdShuffle**

``` 
<iframe allowTransparency="true" frameborder="0" scrolling="no"
marginheight="0" marginwidth="0" topmargin="0" leftmargin="0" width="728"
height="90"
src="http://this.content.served.by.adshuffle.com/p/kl/01/234/r/56/7/8/abdef/ghijkl/view.md?${CACHEBUSTER}&ASTPCT=${CLICK_URL}"></iframe>
```

**Adtech**

``` 
<!--IFRAME Tag (General Redirect) // Page: 728x90 //  -->
<IFRAME WIDTH="728" HEIGHT="90" SCROLLING="No" FRAMEBORDER="0" MARGINHEIGHT="0" MARGINWIDTH="0" SRC="http://adserver.adtech.de/adiframe|3.0|1234|1234|0|1234|ADTECH;AdId=1234;BnId=-1;;target=_blank;misc=[timestamp];rdclick=${CLICK_URL}"><script language="javascript" src="http://adserver.adtech.de/addyn|3.0|1234|1234|0|1234|ADTECH;AdId=1234;BnId=-1;;loc=700;target=_blank;misc=[timestamp];rdclick=${CLICK_URL}"></script><noscript><a href="http://adserver.adtech.de/adlink|3.0|1234|1234|0|1234|ADTECH;AdId=9479763;BnId=-1;;loc=300;misc=[timestamp]" target="_blank;AdId=9479763;BnId=-1;"><img src="media/adserv|3.0|1234|1234|0|1234|ADTECH;loc=300;misc=[timestamp]" border="0" width="728" height="90"></a></noscript></IFRAME>
<!-- End of IFRAME Tag -->
```

**Xandr**

If you are using a Xandr placement tag as a creative, please use this format:

``` 
<!-- BEGIN JS TAG - 728x90 < - DO NOT MODIFY --> <SCRIPT SRC="http://ib..com/ttj?id=1812103&cb=${CACHEBUSTER}&pubclick=${CLICK_URL_ENC}" TYPE="text/javascript"></SCRIPT>
<!-- END TAG -->
```

**Atlas (New)**

``` 
<script src='http://ad.atdmt.com/i/a.js;p=11002201227900;cache=${CACHEBUSTER}?click=${CLICK_URL_ENC}'></script><noscript><iframe frameborder='0' scrolling='no' marginheight='0' marginwidth='0' topmargin='0' leftmargin='0' allowtransparency='true' height='250' width='300' src='http://ad.atdmt.com/i/a.md;p=11002201227900;cache=${CACHEBUSTER}?click=${CLICK_URL_ENC}'></iframe></noscript>
```

**Atlas**

``` 
<iframe src="http://view.atdmt.com/CNT/iview/1234567890/direct;wi.160;hi.600/01${CACHEBUSTER}?click=${CLICK_URL}" frameborder="0" scrolling="no"
marginheight="0" marginwidth="0" topmargin="0" leftmargin="0" allowtransparency="true" width="160" height="600">
<script language="JavaScript" type="text/javascript"> document.write('<a href="${CLICK_URL}http://clk.atdmt.com/CNT/go/1234567890/direct;wi.160;hi.600/01/"
target="_blank"><img src="media/${CACHEBUSTER}"/></a>');
</script><noscript><a href="${CLICK_URL}http://clk.atdmt.com/CNT/go/195860978/direct;wi.160;hi.600/01/" target="_blank"><img border="0"
src="http://view.atdmt.com/CNT/view/1234567890/direct;wi.160;hi.600/01/${CACHEBUSTER}" /></a></noscript></iframe>
```

**DoubleClick**

``` 
<script language="JavaScript" src="http://ad.doubleclick.net/adj/1234.567.890/;net=123456;sz=728x90;click=${CLICK_URL};ord=${CACHEBUSTER}?"
type="text/javascript"></script><noscript><a href="${CLICK_URL}http://ad.doubleclick.net/jump/1234.567.890/;net=123456;sz=728x90;ord=${CACHEBUSTER}?"
target="_blank"><img src="media/;net=123456;sz=728x90;ord=${CACHEBUSTER}?" width="728" height="90" border="0"
alt=""></a></noscript>
```

> [!NOTE]
> If you need to pass an encoded URL in a DoubleClick tag, please use the `{CLICK_URL_ENC}` macro.

**DoubleClick (New Ins Tag)**

``` 
<ins class='dcmads' style='display:inline-block;width:728px;height:90px'
   data-dcm-placement='N3241.163472.EXAMPLEAD/B8852666.112976410'
   data-dcm-rendering-mode='script'
   data-dcm-https-only
   data-dcm-click-tracker=${CLICK_URL}>
 <script src='//www.googletagservices.com/dcm/dcmads.js'></script>
</ins>
```

> [!NOTE]
> The ins type tag does not require the use of Cachebuster macro, as DCM will always fill this automatically.

**DoubleVerify**

DoubleVerify's tags will wrap around your adserver's tag. So, if you're using DoubleVerify with Atlas, the tag would look like the following code. Note that the Atlas tag is contained within the `this.tagsrc` variable. `This.altrc` should be altered to contain a clickable PSA, otherwise the creative will be rejected. Consult with your DoubleVerify rep for more information on how to implement the alternate PSA.

``` 
<script language="javascript" type="text/javascript">
new function() {
this.rand = Math.floor((Math.random() + "") * 1000000000000);
this.dvparams = 'ctx=111111&cmp=22222222&plc=3333333333&sid=444444444';
this.dvregion = '0';
this.tagsrc = <iframe src="http://view.atdmt.com/CNT/iview/1234567890/direct;wi.160;hi.600/01${CACHEBUSTER}?click=${CLICK_URL}" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" topmargin="0" leftmargin="0" allowtransparency="true" width="160" height="600"> <scr'+'ipt language="Javascr'+'ipt" type="text/javascr'+'ipt"> document.write('\'&lt;a href="${CLICK_URL}http://clk.atdmt.com/CNT/go/1234567890/direct;wi.160;hi.600/01/" target="_blank"&gt;&lt;img src="http://view.atdmt.com/CNT/view/195860978/direct;wi.160;hi.600/01/${CACHEBUSTER}"/&gt;&lt;/a&gt;\');</scr'+'ipt><noscr'+'ipt><a href="${CLICK_URL}http://clk.atdmt.com/CNT/go/1111111111/direct;wi.160;hi.600/01/" target="_blank"><img border="0" src="http://view.atdmt.com/CNT/view/1234567890/direct;wi.160;hi.600/01/${CACHEBUSTER}" /></a></noscr'+'ipt></iframe>';
this.altsrc = '<style>\n .container {\n border: 1px solid #3b599e;\n overflow: hidden;\n filter: progid:DXImageTransform.Microsoft.gradient(startColorstr=\'#315d8c\',
endColorstr=\'#84aace\'); /* for IE */\n background: -webkit-gradient(linear, left top, left bottom, from(#315d8c), to(#84aace)); /* for webkit browsers */\n
background: -moz-linear-gradient(top, #315d8c, #84aace); /* for firefox 3.6+ */ \n }\n .cloud {\n color: #fff;\n position: relative;\n font: 100%
"Times New Roman", Times, serif;\n text-shadow: 0px 0px 10px #fff;\n line-height: 0;\n }\n </style>\n <scr'+'ipt type="text/javascr'+'ipt">\n
function cloud()
{\n var b1 = "<div class=\\"cloud\\" style=\\"font-size: ";\n var b2 = "px; position: absolute; top: ";\n
document.write(b1+"300px; width: 300px; height: 300"+b2+"34px; left: 28px;\\">.<\\/div>");\n document.write(b1+"300px; width: 300px; height:
300"+b2+"46px; left: 10px;\\">.<\\/div>");\n document.write(b1+"300px; width: 300px; height: 300"+b2+"46px; left: 50px;\\">.<\\/div>");\n
document.write(b1+"400px; width: 400px; height: 400"+b2+"24px; left: 20px;\\">.<\\/div>");\n }\n
function clouds(){\n var top = [];\n var left = \-10;\n var a1 = "<div style=
\\
"position: relative; top: ";\n
var a2 = "px; left: ";\n var a3 = "px;
\\
"><scr'+'ipt type=\\"text/javascr'+'ipt\\">cloud();<\\/scr'+'ipt><\\/div>";\n fo
r(i=0; i<8; i++)\n {\n
document.write(a1+top[0]\+a2+left+a3);\n document.write(a1+top[1]\+a2+left+a3);\n document.write(a1+top[2]\+a2+left+a3);\n
document.write(a1+top[3]\+a2+left+a3); \n if(i==4)\n {\n left = -90;\n top = [\'0\',\'160\',\'320\',\'480\'];\n }\n else left \+= 160;\n }\n }\n
</scr'+'ipt>\n<div class="container" style="width: 160px; height: 600px;">\n <scr'+'ipt type="text/javascr'+'ipt">clouds();</scr'+'ipt>\n';

this.callbackName = '\__dvredirect_callback_' + this.rand;
var thisRedirect = this;
window[this.callbackName] = function () { return thisRedirect; };

var src = 'http://rtbcdn.doubleverify.com/bsredirect5.js?callback=' + this.callbackName;
document.write('<scr' + 'ipt src=' + src + '></scr' + 'ipt>');
}
</script>
```

**EyeReturn**

``` 
<script type="text/javascript" src="http://voken.eyereturn.com/?144857&click=${CLICK_URL}&params=${CACHEBUSTER}"></script>
```

**Fetchback**

``` 
<script language='javascript' type='text/javascript' src='http://imp.fetchback.com/serve/fb/adtag.js?tid=47476&type=widesky&clicktrack=${CLICK_URL_ENC}'></script>
```

**Flashtalking**

``` 
<script language="Javascript1.1" type="text/javascript">
var ftClick = "${CLICK_URL}";
var ftX = "";
var ftY = "";
var ftZ = "";
var ftContent = "";
var ft160x600_OOBclickTrack = "";
var ftRandom = Math.random()*1000000;
var ftBuildTag1 = "<scr";
var ftBuildTag2 = "</";
var ftTag = ftBuildTag1 + 'ipt language="javascript1.1" type="text/javascript" ';
ftTag += 'src="http://servedby.flashtalking.com/imp/55555;55555;201;js;MediaIQ;Sky160x600/?click='+ftClick+'&ftx='+ftX+'&fty='+ftY+'&ftadz='+ftZ+'&ftscw='+ftContent+'&cachebuster='+ftRandom+'" id="ftscript_160x600" name="ftscript_160x600"';
ftTag += '">' + ftBuildTag2 + 'script>'; document.write(ftTag);
</script>
<noscript>
<a href="${CLICK_URL}http://servedby.flashtalking.com/click/55555;55555;0;209;0/?url=232492" target="_blank">
<img border="0" src="http://servedby.flashtalking.com/imp/55555;55555;205;gif;MediaIQ;Sky160x600/?CB=${CACHEBUSTER}"></a>
</noscript>
```

**Integral Ad science (formerly AdSafe)**

> [!NOTE]
> Please remember to include the IS_PREVIEW macro at the end of the [adsafeprotected](http://fw.adsafeprotected.com/) URLs. Otherwise, the creative will not preview correctly in our Impression Bus and will be rejected in the audit process.
``` 
<script language="JavaScript" type="text/javascript" src="http://fw.adsafeprotected.com/rjss/at/53729/573929/CAT/jview/101010101/direct/01/${CACHEBUSTER}?click=${CLICK_URL}&adsafe_preview=${IS_PREVIEW}">
</script><noscript><a href="${CLICK_URL}http://clk.atdmt.com/CAT/go/101010101/direct/01/" target="_blank"><img border="0" src="http://fw.adsafeprotected.com/rfw/at/53729/573930/CAT/view/101010101/direct/01/${CACHEBUSTER}?adsafe_preview=${IS_PREVIEW}" /></a></noscript>
```

``` 
<IFRAME SRC="http://fw.adsafeprotected.com/rjsi/dc/54321/123456/adi/N1068.151790.ABCDE/B6797568.72;sz=160x600;click=${CLICK_URL};ord=${CACHEBUSTER}?adsafe_preview=${IS_PREVIEW}" WIDTH=160 HEIGHT=600 MARGINWIDTH=0 MARGINHEIGHT=0 HSPACE=0 VSPACE=0 FRAMEBORDER=0 SCROLLING=no BORDERCOLOR='#000000'>
<SCRIPT language='JavaScript1.1' SRC="http://fw.adsafeprotected.com/rjss/dc/54321/455394/adj/N1068.151790.ABCDE/B6797568.72;abr=!ie sz=160x600;click=${CLICK_URL};ord=${CACHEBUSTER}?adsafe_preview=${IS_PREVIEW}">
</SCRIPT>
<NOSCRIPT>
<A HREF="${CLICK_URL}http://ad.doubleclick.net/jump/N1068.151790.ABCDE/B6797568.72;abr=!ie4;abr=!ie5;sz=160x600;ord=${CACHEBUSTER}?">
<IMG SRC="http://fw.adsafeprotected.com/rfw/dc/54321/455392/ad/N1068.151790.ABCDE/B6797568.72;abr=!ie4;abr=!ie5;sz=160x600;ord=${CACHEBUSTER}?adsafe_preview=${IS_PREVIEW}" BORDER=0 WIDTH=160 HEIGHT=600 ALT="Advertisement"></A>
</NOSCRIPT>
</IFRAME>
```

**Integral Ad science (AdSafe) tags in FlashTalking format:**

``` 
<noscript>
<a href="${CLICK_URL}http://example.com/click/5/25684;564938;0;209;0/?ft_width=300&ft_height=250&url=3747563" target="_blank">
<img border="0" src="http://fw.adsafeprotected.com/rfw/example.com/16786/959163/imp/5/25684;564938;205;gif;Client;300x250Myblocking/?adsafe_preview=${IS_PREVIEW}"></a>
</noscript>
<script language="Javascript1.1" type="text/javascript">
var ftClick = "${CLICK_URL}";
var ftX = "";
var ftY = "";
var ftZ = "";
var ftOBA = 1;
var ftContent = "";
var ftCustom = "";
var ft300x250_OOBclickTrack = "";
var ftRandom = Math.random()*1000000;
var ftBuildTag1 = "<scr";
var ftBuildTag2 = "</";
if(typeof(ft_referrer)=="undefined"){var ft_referrer=(function(){var r="";
if(window==top){r=window.location.href;}
else{try{r=window.parent.location.href;}catch(e){}r=(r)?r:document.referrer;}while(escape(r).length>1500){r=r.substring(0,r.length-1);}return r;}());}
var ftDomain = (window==top)?"":document.referrer?"&ft_ifb=1&ft_domain="+escape(document.referrer.match("(?::q/q/)+([qw-]+(q.[qw-]+)+)(q/)?".replace(/q/g,unescape("%"+"5C")))[1]):"";
var ftTag = ftBuildTag1 + 'ipt language="javascript1.1" type="text/javascript" ';ftTag += 'src="http://fw.adsafeprotected.com/rjss/example.com/16786/959165/imp/5/25684;564938;201;js;Client;300x250Myblocking/?ftx='+ftX+'&fty='+ftY+'&ftadz='+ftZ+'&ftscw='+ftContent+'&ft_custom='+ftCustom+'&click='+ftClick+'&ftOBA='+ftOBA+ftDomain+'&ft_referrer='+escape(ft_referrer)+'&cachebuster='+ftRandom+'&adsafe_preview=${IS_PREVIEW}" id="ftscript_300x250" name="ftscript_300x250"';ftTag += '>' + ftBuildTag2 + 'script>';
document.write(ftTag);
</script>
```

**Integral Ad science in MediaMind format:**

``` 
<script src="http://fw.adsafeprotected.com/rjss/bs.serving-sys.com/20286/1398936/BurstingPipe/adServer.bs?cn=rsb&c=12&pli=123456&PluID=0&w=120&h=600&ord=${CACHEBUSTER}&ucm=true&ncu=$$${CLICK_URL_ENC}$$?adsafe_preview=${IS_PREVIEW}"></script>
<noscript><a href="${CLICK_URL}http://bs.serving-sys.com/BurstingPipe/adServer.bs%3Fcn%3Dbrd%26FlightID%3D123456%26Page%3D%26PluID%3D0%26Pos%3D1234" target="_blank"><img src="media/adServer.bs?cn=bsr&FlightID=7872095&Page=&PluID=0&Pos=1756162582&adsafe_preview=${IS_PREVIEW}" border=0 width=120 height=600></a></noscript>
```

**Sizmek (formerly MediaMind)**

``` 
<script src="http://bs.serving-sys.com/BurstingPipe/adServer.bs?cn=rsb&c=12&pli=1234567&PluID=0&w=728&h=90&ord=${CACHEBUSTER}&ifrm=-1&ucm=true&ncu=$$${CLICK_URL_ENC}$$">
</script><noscript><a href="${CLICK_URL}http%3A//bs.serving-sys.com/BurstingPipe/BannerRedirect.asp%3FFlightID%3D1234567%26Page%3D%26PluID%3D0%26Pos%3D1234"
target="_blank"><img src="media/BannerSource.asp?FlightID=1234567&Page=&PluID=0&Pos=1234" border=0 width=728
height=90></a></noscript>
```

**MediaPlex**

``` 
<script type="text/javascript" src="http://altfarm.mediaplex.com/ad/js/12345-678901-23456-7?mpt=${CACHEBUSTER}&mpvc=${CLICK_URL_ENC}"></script>
<noscript><a href="${CLICK_URL}http://altfarm.mediaplex.com/ad/nc/12345-678901-23456-7?mpt=${CACHEBUSTER}">
<img src="media/12345-678901-23456-7?mpt=${CACHEBUSTER}" alt="Click Here" border="0"></a></noscript>
<IFRAME SRC="http://b3.mookie1.com/2/abcdefg/hijkl/123456/Banner/300/1${CACHEBUSTER}@x90" WIDTH=0 HEIGHT=0 MARGINWIDTH=0
MARGINHEIGHT=0 HSPACE=0 VSPACE=0 FRAMEBORDER=0 SCROLLING=no BORDERCOLOR="#000000"></IFRAME>
```

**Open Ad stream (24/7)**

``` 
<script LANGUAGE="JavaScript1.1"
SRC="http://oasn04.247realmedia.com/RealMedia/ads/adstream_jx.ads/XXXXX/XXXXX/XXXXX/XXXXX/300/1${CACHEBUSTER}@x90?${CLICK_URL}">
</script>
```

**PointRoll**

```
<script type="text/javascript">
function pr_swfver(){
var osf,osfd,i,axo=1,v=0,nv=navigator;
if(nv.plugins&&nv.mimeTypes.length){osf=nv.plugins["Shockwave Flash"];if(osf&&osf.description){osfd=osf.description;v=parseInt(osfd.substring(osfd.indexOf(".")-2))}}
else{try{for(i=5;axo!=null;i++){axo=new ActiveXObject("ShockwaveFlash.ShockwaveFlash."+i);v=i}}catch(e){}}
return v;
}
var pr_d=new Date();pr_d=pr_d.getDay()+"|"+pr_d.getHours()+":"+pr_d.getMinutes()+"|"+-pr_d.getTimezoneOffset()/60;
var pr_postal="";
var pr_data="";var pr_ies="";

var pr_redir="${CLICK_URL}$CTURL$";

var pr_nua=navigator.userAgent.toLowerCase();
var prHost=(("https:"==document.location.protocol)?"https://":"http://");var pr_sec=((prHost=='https://')?'&secure=1':'');
var pr_pos="",pr_inif=(window!=top);
if(pr_inif){try{pr_pos=(typeof(parent.document)!="unknown")?(((typeof(inDapIF)!="undefined")&&(inDapIF))||(parent.document.domain==document.domain))?"&pos=s":"&pos=x":"&pos=x";}
catch(e){pr_pos="&pos=x";}if(pr_pos=="&pos=x"){var pr_u=new RegExp("[A-Za-z]+:[/][/][A-Za-z0-9.-]+");var pr_t=this.window.document.referrer;
var pr_m=pr_t.match(pr_u);if(pr_m!=null){pr_pos+="&dom="+pr_m[0];}}else{if(((typeof(inDapMgrIf)!="undefined")&&(inDapMgrIf))||((typeof(isAJAX)!="undefined")&&(isAJAX))){pr_pos+="&ajx=1"}}}
if(pr_postal!=""){var przipmatch=/^\d{5}$/;if(przipmatch.test(pr_postal)){pr_pos+="&postal="+pr_postal;}}
if((pr_data!="")&&(pr_data.indexOf("&")<0)){pr_pos+="&data="+pr_data;}
if((pr_ies!="")&&(pr_ies.indexOf("&")<0)){pr_pos+="&ies="+pr_ies;}
var pr_s="ads.pointroll.com/PortalServe/?pid=xxxx&flash="+pr_swfver()+"&time="+pr_d+"&redir="+pr_redir+pr_pos+pr_sec+"&r="+Math.random();
document.write("<scr"+"ipt type='text/javascript' src='"+prHost+pr_s+"'></scr"+"ipt>");
</script>
```

**Project sunblock**

> [!NOTE]
> When previewing Project Sunblock tags, please ensure you deselect Serve in iFrame as this will stop the tags previewing in our UI and you will be unable to test click-tracking.

``` 
<script type='text/javascript'>
    var _sblq = _sblq || [];
    (function() {
        var s = document.getElementsByTagName('script'), s0 = s[0], adElement = s[s.length-1];
        var sl = Math.random().toString(36).substring(2);
        _sblq.push([sl, 'setClickUrl', '${CLICK_URL}']);
        _sblq.push([sl, 'displayAd', adElement,300, 1234]);
        var sb = document.createElement('script'); sb.type = 'text/javascript'; sb.async = true; sb.defer = true;
        sb.src = ('http:'==document.location.protocol ? "http:" : "https:")+'//js.sblk.io/sb.js';
        s0.parentNode.insertBefore(sb, s0);
    })();
</script>
<noscript><img src='//api.sblk.io/request.gif?campaign_id=000&ad_id=0000' width='1' height='1'></noscript>
```

**SmartAdServer**

``` 
<SCRIPT LANGUAGE="JavaScript1.1" SRC="http://ww856.smartadserver.com/call/adj/306890/2591652/CLIENT.campaign/600x300/${CACHEBUSTER}/no?${CLICK_URL}"></SCRIPT>
<NOSCRIPT><a href="${CLICK_URL}http://ww856.smartadserver.com/call/jumpi/306343/2591652/CLIENT.campaign/600x300/${CACHEBUSTER}/no?" target="_blank">
<img src="media/no?" border="0"></a></NOSCRIPT>
```

**Trade doubler**

``` 
<script type="text/javascript">
var uri = 'http://impde.tradedoubler.com/imp?type(iframe)g(18906306)a(1838453)preurl(${CLICK_URL})' + new String (Math.random()).substring (2, 11);
document.write('<iframe src="'+uri +'" width="160" height="600" frameborder="0" border="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>');
</script>
```

**Traffiq**

``` 
<iframe src="http://ads.traffiq.com/ad.imp?pid=1234&oid=5678&rand=${CACHEBUSTER}/?pclk=${CLICK_URL}" width="728" height="90"
frameborder="0" marginheight="0" marginwidth="0" scrolling="no" topmargin="0" leftmargin="0"> </iframe>
```

**Weborama**

``` 
<a href="${CLICK_URL}http://gae.solution.weborama.fr/fcgi-bin/dispatch.fcgi?a.A=cl&a.si=54&a.te=56&a.ra=__RANDOM__&a.im=1&g.lu=" target="_blank">
<img src="media/dispatch.fcgi?a.A=im&a.si=54&a.te=56&a.he=600&a.wi=160&a.ra=__RANDOM__&a.hr=R" width="160" height="600"></a>
```

**Yield manager**

``` 
<IFRAME FRAMEBORDER=0 MARGINWIDTH=0 MARGINHEIGHT=0 SCROLLING=NO WIDTH=300 HEIGHT=250 SRC="http://ad.yieldmanager.com/st?ad_type=iframe&ad_size=300x250&section=XXXXXXX&pub_redirect_unencoded=1&pub_redirect=${CLICK_URL}"></IFRAME>
```

**Zedo**

``` 
<script language="JavaScript" src="http://d7.zedo.com/jsc/d3/fl.js?n=809&c=1839/1740&s=704&d=14&w=728&h=90&l=${CLICK_URL}&z=${CACHEBUSTER}"></script> <noscript><a href="http://yads.zedo.com/ads2/r?n=809;c=1839/1740;s=704;x=3584;u=j;z=${CACHEBUSTER}" target="_blank"><img

 border="0" width="728" height="90" src="http://yads.zedo.com/ads2/x?n=809;c=1839/1740;s=704;x=3584;u=j;z=${CACHEBUSTER}" alt="Click here"></a> </noscript>
```

**ViralGains odyssey**

``` 
<iframe src = 'https://odc-wsb.viralgains.com?lineItemId=1234abcd&vendorId=1234abcd&creativeId=1234abcd&cachebuster=${VG_CACHEBUSTER}&clickURLEnc=${CLICK_URL_ENC}' width='xxx' height='yyy' frameborder='0' marginheight='0' marginwidth='0' target='_blank' scrolling='no'></iframe>
```

> [!NOTE]
> If the ad server you use is not listed here and you already know the correct placement for the macros in your tag, [contact us](https://help.appnexus.com/) to have an example for that ad server added to the list. Ensure that you provide:
>
> - The name of the ad server the tags appear on.
> - The exact parameters used to traffic the click tracking and cache busting macros (if you don't know which parameters are used, contact your client to obtain them).
