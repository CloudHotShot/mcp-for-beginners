<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "382fddb4ee4d9c1bdc806e2ee99b70c8",
  "translation_date": "2025-07-17T12:50:44+00:00",
  "source_file": "02-Security/README.md",
  "language_code": "my"
}
-->
# လုံခြုံရေးအကောင်းဆုံးလေ့လာမှုများ

Model Context Protocol (MCP) ကို အသုံးပြုခြင်းဖြင့် AI အခြေပြု အက်ပလီကေးရှင်းများတွင် အင်အားကြီးသော စွမ်းဆောင်ရည်အသစ်များရရှိနိုင်သော်လည်း၊ ရိုးရာဆော့ဖ်ဝဲလ်အန္တရာယ်များထက် ပိုမိုထူးခြားသော လုံခြုံရေး စိန်ခေါ်မှုများကိုလည်း ဖြစ်ပေါ်စေပါသည်။ လုံခြုံရေးကုဒ်ရေးခြင်း၊ အနည်းဆုံးခွင့်ပြုချက်၊ နှင့် ပစ္စည်းလမ်းကြောင်းလုံခြုံရေးကဲ့သို့ ရှိပြီးသား စိုးရိမ်ချက်များအပြင် MCP နှင့် AI အလုပ်များတွင် prompt injection, tool poisoning, dynamic tool modification, session hijacking, confused deputy attacks, နှင့် token passthrough အန္တရာယ်များကဲ့သို့သော အသစ်သော အန္တရာယ်များလည်း ရှိပါသည်။ ဤအန္တရာယ်များကို မှန်ကန်စွာ စီမံမထားပါက ဒေတာထွက်ပေါက်ခြင်း၊ ကိုယ်ရေးကိုယ်တာ လုံခြုံမှုချိုးဖောက်ခြင်း၊ နှင့် မရည်ရွယ်ထားသော စနစ်အပြုအမူများ ဖြစ်ပေါ်နိုင်ပါသည်။

ဤသင်ခန်းစာတွင် MCP နှင့်ဆက်စပ်သော အရေးကြီးဆုံး လုံခြုံရေးအန္တရာယ်များကို (authentication, authorization, အလွန်အကျွံခွင့်ပြုချက်များ, အတိုက်ရိုက်မဟုတ်သော prompt injection, session လုံခြုံရေး, confused deputy ပြဿနာများ, token passthrough အန္တရာယ်များ, နှင့် ပစ္စည်းလမ်းကြောင်း အန္တရာယ်များ) လေ့လာပြီး၊ ထိုအန္တရာယ်များကို လျော့နည်းစေရန် လုပ်ဆောင်နိုင်သော ထိန်းချုပ်မှုများနှင့် အကောင်းဆုံးလေ့လာမှုများကို ပေးပါသည်။ Microsoft ၏ Prompt Shields, Azure Content Safety, နှင့် GitHub Advanced Security ကဲ့သို့သော ဖြေရှင်းနည်းများကို အသုံးပြု၍ MCP ကို ပိုမိုခိုင်မာစေရန်လည်း သင်ယူနိုင်ပါသည်။ ဤထိန်းချုပ်မှုများကို နားလည်ပြီး အသုံးချခြင်းဖြင့် လုံခြုံရေးချိုးဖောက်မှု ဖြစ်ပေါ်နိုင်မှုကို အလွန်လျော့နည်းစေပြီး သင့် AI စနစ်များကို ခိုင်မာယုံကြည်စိတ်ချရစေပါသည်။

# သင်ယူရမည့် ရည်မှန်းချက်များ

ဤသင်ခန်းစာအဆုံးတွင် သင်သည် -

- Model Context Protocol (MCP) မှ ဖြစ်ပေါ်လာသော ထူးခြားသော လုံခြုံရေးအန္တရာယ်များကို ရှာဖွေရှင်းလင်းနိုင်မည်၊ ၎င်းတွင် prompt injection, tool poisoning, အလွန်အကျွံခွင့်ပြုချက်များ, session hijacking, confused deputy ပြဿနာများ, token passthrough အန္တရာယ်များ, နှင့် ပစ္စည်းလမ်းကြောင်း အန္တရာယ်များ ပါဝင်သည်။
- MCP လုံခြုံရေးအန္တရာယ်များအတွက် ထိရောက်သော ထိန်းချုပ်မှုများကို ဖော်ပြနိုင်ပြီး အသုံးချနိုင်မည်၊ ဥပမာအားဖြင့် ခိုင်မာသော authentication, အနည်းဆုံးခွင့်ပြုချက်, လုံခြုံသော token စီမံခန့်ခွဲမှု, session လုံခြုံရေး ထိန်းချုပ်မှုများ, နှင့် ပစ္စည်းလမ်းကြောင်း စစ်ဆေးမှုများ။
- Microsoft ၏ Prompt Shields, Azure Content Safety, နှင့် GitHub Advanced Security ကဲ့သို့သော ဖြေရှင်းနည်းများကို နားလည်ပြီး MCP နှင့် AI အလုပ်များကို ကာကွယ်နိုင်မည်။
- Tool metadata ကို စစ်ဆေးခြင်း၊ dynamic ပြောင်းလဲမှုများကို စောင့်ကြည့်ခြင်း၊ အတိုက်ရိုက်မဟုတ်သော prompt injection တိုက်ခိုက်မှုများကို ကာကွယ်ခြင်း၊ နှင့် session hijacking ကို တားဆီးခြင်း၏ အရေးပါမှုကို သိရှိနိုင်မည်။
- လုံခြုံရေးအကောင်းဆုံးလေ့လာမှုများဖြစ်သော secure coding, server hardening, နှင့် zero trust architecture များကို MCP အကောင်အထည်ဖော်မှုတွင် ပေါင်းစပ်အသုံးပြု၍ လုံခြုံရေးချိုးဖောက်မှု ဖြစ်ပေါ်နိုင်မှုနှင့် ထိခိုက်မှုကို လျော့နည်းစေနိုင်မည်။

# MCP လုံခြုံရေး ထိန်းချုပ်မှုများ

အရေးကြီးသော အရင်းအမြစ်များကို ဝင်ရောက်အသုံးပြုနိုင်သော စနစ်တိုင်းတွင် လုံခြုံရေး စိန်ခေါ်မှုများ ရှိသည်။ လုံခြုံရေး စိန်ခေါ်မှုများကို အခြေခံ လုံခြုံရေး ထိန်းချုပ်မှုများနှင့် အယူအဆများကို မှန်ကန်စွာ အသုံးချခြင်းဖြင့် ဖြေရှင်းနိုင်သည်။ MCP သည် အသစ်တင်သတ်မှတ်ထားသည့် ပရိုတိုကောဖြစ်သောကြောင့် သတ်မှတ်ချက်များသည် အလွန်လျင်မြန်စွာ ပြောင်းလဲနေပြီး ပရိုတိုကောတိုးတက်မှုနှင့်အမျှ လုံခြုံရေး ထိန်းချုပ်မှုများလည်း တိုးတက်လာမည်ဖြစ်သည်။ နောက်ဆုံးတွင် ၎င်းတို့သည် စီးပွားရေးအဖွဲ့အစည်းများနှင့် ရှိပြီးသား လုံခြုံရေး ဖွဲ့စည်းပုံများနှင့် အကောင်းဆုံးလေ့လာမှုများနှင့် ပိုမိုကောင်းမွန်စွာ ပေါင်းစည်းနိုင်မည်ဖြစ်သည်။

[Microsoft Digital Defense Report](https://aka.ms/mddr) တွင် ထုတ်ပြန်ထားသည့် သုတေသနအရ ၉၈% အထိ လုံခြုံရေးချိုးဖောက်မှုများကို ခိုင်မာသော လုံခြုံရေးစနစ်နှင့် ကာကွယ်နိုင်ပြီး၊ လုံခြုံရေးချိုးဖောက်မှု မည်သည့်အမျိုးအစားမဆို ကာကွယ်ရန် အကောင်းဆုံးနည်းလမ်းမှာ မူလ လုံခြုံရေးစနစ်၊ secure coding အကောင်းဆုံးလေ့လာမှုများနှင့် ပစ္စည်းလမ်းကြောင်း လုံခြုံရေးကို မှန်ကန်စွာ လုပ်ဆောင်ခြင်းဖြစ်သည်။ ယင်းနည်းလမ်းများသည် လုံခြုံရေးအန္တရာယ် လျော့နည်းစေရန် အကျိုးသက်ရောက်မှု အများဆုံးဖြစ်သည်။

MCP ကို အသုံးပြုစဉ် လုံခြုံရေးအန္တရာယ်များကို မည်သို့ စတင်ဖြေရှင်းနိုင်မည်ကို ကြည့်ကြရအောင်။

> **Note:** အောက်ပါ အချက်အလက်များသည် **၂၀၂၅ ခုနှစ် မေ ၂၉ ရက်** အခြေအနေအရ မှန်ကန်ပါသည်။ MCP ပရိုတိုကောသည် ဆက်လက်တိုးတက်နေပြီး နောင်လာမည့် အကောင်အထည်ဖော်မှုများတွင် အသစ်သော authentication ပုံစံများနှင့် ထိန်းချုပ်မှုများ ပါဝင်နိုင်ပါသည်။ နောက်ဆုံးရ အချက်အလက်များနှင့် လမ်းညွှန်ချက်များအတွက် [MCP Specification](https://spec.modelcontextprotocol.io/) နှင့် တရားဝင် [MCP GitHub repository](https://github.com/modelcontextprotocol) နှင့် [security best practice page](https://modelcontextprotocol.io/specification/draft/basic/security_best_practices) ကို အမြဲတမ်း ရှာဖွေကြည့်ပါ။

### ပြဿနာဖော်ပြချက်  
မူလ MCP သတ်မှတ်ချက်တွင် ဖန်တီးသူများသည် ကိုယ်ပိုင် authentication server ကိုရေးသားမည်ဟု သတ်မှတ်ထားသည်။ ၎င်းသည် OAuth နှင့် ဆက်စပ်သော လုံခြုံရေး ကန့်သတ်ချက်များကို သိရှိထားရန် လိုအပ်သည်။ MCP server များသည် OAuth 2.0 Authorization Server အဖြစ် လုပ်ဆောင်ကာ အသုံးပြုသူ authentication ကို တိုက်ရိုက် စီမံခန့်ခွဲသည်၊ Microsoft Entra ID ကဲ့သို့သော ပြင်ပဝန်ဆောင်မှုသို့ မပေးအပ်ပါ။ **၂၀၂၅ ခုနှစ် ဧပြီ ၂၆ ရက်** တွင် MCP သတ်မှတ်ချက်ကို အပ်ဒိတ်ပြုလုပ်ပြီး MCP server များသည် အသုံးပြုသူ authentication ကို ပြင်ပဝန်ဆောင်မှုသို့ ပေးအပ်နိုင်ရန် ခွင့်ပြုထားသည်။

### အန္တရာယ်များ
- MCP server တွင် authorization logic မမှန်ကန်စွာ ဖွဲ့စည်းထားခြင်းကြောင့် အချက်အလက်များ ထွက်ပေါက်ခြင်းနှင့် မမှန်ကန်သော access control များ ဖြစ်ပေါ်နိုင်သည်။
- OAuth token ကို MCP server တွင် ခိုးယူခြင်း။ ခိုးယူထားသော token ဖြင့် MCP server ကို မူရင်း server အဖြစ် လိမ်လည်အသုံးပြု၍ ဝန်ဆောင်မှုနှင့် ဒေတာများကို ဝင်ရောက်နိုင်သည်။

#### Token Passthrough  
Authorization သတ်မှတ်ချက်တွင် token passthrough ကို တိတိကျကျ တားမြစ်ထားပြီး အောက်ပါ လုံခြုံရေးအန္တရာယ်များ ဖြစ်ပေါ်စေပါသည်။

#### လုံခြုံရေး ထိန်းချုပ်မှုများကို လွှဲချော်ခြင်း  
MCP Server သို့မဟုတ် downstream API များသည် token audience သို့မဟုတ် အခြား credential ကန့်သတ်ချက်များပေါ် မူတည်၍ rate limiting, request validation, traffic monitoring ကဲ့သို့သော လုံခြုံရေး ထိန်းချုပ်မှုများကို အရေးကြီးစွာ အကောင်အထည်ဖော်နိုင်သည်။ Clients များသည် MCP server မှ token မမှန်ကန်စွာ စစ်ဆေးခြင်းမရှိဘဲ တိုက်ရိုက် downstream API များနှင့် token များကို အသုံးပြုနိုင်ပါက ထိုထိန်းချုပ်မှုများကို လွှဲချော်နိုင်သည်။

#### တာဝန်ယူမှုနှင့် စစ်ဆေးမှု ပြဿနာများ  
MCP Server သည် upstream မှ ထုတ်ပေးသော access token ဖြင့် ခေါ်ဆိုသော MCP Clients များကို ခွဲခြားနိုင်ခြင်း မရှိပါ။  
Downstream Resource Server ၏ မှတ်တမ်းများတွင် token များကို ပေးပို့နေသော MCP server မဟုတ်သော အခြား အရင်းအမြစ်မှ တောင်းဆိုမှုများအဖြစ် ပြသနိုင်သည်။  
ဤအချက်များကြောင့် ဖြစ်ရပ်စစ်ဆေးခြင်း၊ ထိန်းချုပ်မှုများနှင့် စစ်ဆေးမှုများ ခက်ခဲစေပါသည်။  
MCP Server သည် token များ၏ အခွင့်အရေးများ (ဥပမာ roles, privileges, audience) သို့မဟုတ် အခြား metadata များကို စစ်ဆေးခြင်းမပြုဘဲ token များကို ပေးပို့ပါက ခိုးယူထားသော token ကိုင်ဆောင်ထားသူ မကောင်းဆိုးရွားသူသည် MCP Server ကို ဒေတာထွက်ပေါက်အတွက် proxy အဖြစ် အသုံးပြုနိုင်သည်။

#### ယုံကြည်မှုနယ်နိမိတ် ပြဿနာများ  
Downstream Resource Server သည် အထူးသီးသန့် အဖွဲ့အစည်းများအား ယုံကြည်မှု ပေးသည်။ ယုံကြည်မှုတွင် မူလအရင်းအမြစ် သို့မဟုတ် client အပြုအမူ ပုံစံများအပေါ် အခြေခံထားသည်။ ယုံကြည်မှုနယ်နိမိတ်ကို ချိုးဖောက်ခြင်းသည် မမျှော်လင့်ထားသော ပြဿနာများ ဖြစ်ပေါ်စေနိုင်သည်။  
Token ကို ဝန်ဆောင်မှုများစွာမှ လက်ခံပြီး မှန်ကန်စွာ စစ်ဆေးခြင်းမရှိပါက ဝန်ဆောင်မှုတစ်ခုကို ခိုးယူသူသည် token ကို အသုံးပြု၍ အခြား ဝန်ဆောင်မှုများကို ဝင်ရောက်နိုင်သည်။

#### အနာဂတ် ကိုက်ညီမှု အန္တရာယ်  
ယနေ့ MCP Server သည် "pure proxy" အဖြစ် စတင်ခဲ့ပါကလည်း နောင်လာမည့်အချိန်တွင် လုံခြုံရေး ထိန်းချုပ်မှုများ ထပ်မံ ထည့်သွင်းရန် လိုအပ်နိုင်သည်။ token audience ကို မှန်ကန်စွာ ခွဲခြားထားခြင်းဖြင့် လုံခြုံရေး မော်ဒယ် တိုးတက်ရန် ပိုမိုလွယ်ကူစေသည်။

### လျော့နည်းစေရန် ထိန်းချုပ်မှုများ

**MCP server များသည် MCP server အတွက် တိတိကျကျ ထုတ်ပေးထားသော token မဟုတ်သော token များကို လက်ခံမရပါ။**

- **Authorization Logic ကို ပြန်လည်သုံးသပ်ပြီး ခိုင်မာစေပါ:** MCP server ၏ authorization အကောင်အထည်ဖော်မှုကို သေချာစွာ စစ်ဆေး၍ ရည်ရွယ်ထားသော အသုံးပြုသူများနှင့် client များသာ အရေးကြီးသော အရင်းအမြစ်များကို ဝင်ရောက်နိုင်စေရန် သေချာစေပါ။ လက်တွေ့ လမ်းညွှန်ချက်များအတွက် [Azure API Management Your Auth Gateway For MCP Servers | Microsoft Community Hub](https://techcommunity.microsoft.com/blog/integrationsonazureblog/azure-api-management-your-auth-gateway-for-mcp-servers/4402690) နှင့် [Using Microsoft Entra ID To Authenticate With MCP Servers Via Sessions - Den Delimarsky](https://den.dev/blog/mcp-server-auth-entra-id-session/) ကို ကြည့်ရှုပါ။
- **လုံခြုံသော Token အသုံးပြုမှုများကို အကောင်အထည်ဖော်ပါ:** [Microsoft ၏ token စစ်ဆေးခြင်းနှင့် အသက်တာကာလအကောင်းဆုံးလေ့လာမှုများ](https://learn.microsoft.com/en-us/entra/identity-platform/access-tokens) ကို လိုက်နာကာ access token မမှန်ကန်စွာ အသုံးပြုခြင်းနှင့် token ပြန်လည်အသုံးပြုခြင်း၊ ခိုးယူခြင်း အန္တရာယ်များကို လျော့နည်းစေပါ။
- **Token သိမ်းဆည်းမှုကို ကာကွယ်ပါ:** Token များကို အမြဲတမ်း လုံခြုံစွာ သိမ်းဆည်းပြီး သိုလှောင်ရာတွင် နှင့် လမ်းကြောင်းပေါ်တွင် စာရင်းအင်းကာကွယ်မှု (encryption) ကို အသုံးပြုပါ။ အကောင်အထည်ဖော်နည်းများအတွက် [Use secure token storage and encrypt tokens](https://youtu.be/uRdX37EcCwg?si=6fSChs1G4glwXRy2) ကို ကြည့်ရှုပါ။

# MCP server များအတွက် အလွန်အကျွံခွင့်ပြုချက်များ

### ပြဿနာဖော်ပြချက်  
MCP server များသည် ဝင်ရောက်နေသော ဝန်ဆောင်မှု/အရင်းအမြစ်များအတွက် အလွန်အကျွံခွင့်ပြုချက်များ ရရှိထားနိုင်သည်။ ဥပမာအားဖြင့် AI အရောင်းဆိုင်ရာ အက်ပလီကေးရှင်းတစ်ခုတွင် ပါဝင်သော MCP server သည် စီးပွားရေး ဒေတာသိုလှောင်ရာမှ အရောင်းဒေတာများကိုသာ ဝင်ရောက်ခွင့်ရှိပြီး သိုလှောင်ရာရှိ ဖိုင်အားလုံးကို မဝင်ရောက်ခွင့်မရှိသင့်ပါ။ အနည်းဆုံးခွင့်ပြုချက် သဘောတရား (least privilege) ကို ပြန်လည်ဆန်းစစ်ပါက တာဝန်ထမ်းဆောင်ရန် လိုအပ်သည့် ခွင့်ပြုချက်ထက် မပိုရသင့်ပါ။ AI သည် လွယ်ကူပြောင်းလဲနိုင်စေရန်အတွက် လိုအပ်သည့် ခွင့်ပြုချက်များကို တိတိကျကျ သတ်မှတ်ရန် အခက်အခဲများ ရှိသည်။

### အန္တရာယ်များ  
- အလွန်အကျွံခွင့်ပြုချက်များ ပေးခြင်းကြောင့် MCP server မရည်ရွယ်ထားသော ဒေတာများ ထွက်ပေါက်ခြင်း သို့မဟုတ် ပြင်ဆင်ခြင်း ဖြစ်ပေါ်နိုင်သည်။ ဒါ့အပြင် ဒေတာသည် ကိုယ်ရေးကိုယ်တာ သတင်းအချက်အလက် (PII) ဖြစ်ပါက ကိုယ်ရေးကိုယ်တာ လုံခြုံမှု ပြဿနာ ဖြစ်ပေါ်နိုင်သည်။

### လျော့နည်းစေရန် ထိန်းချုပ်မှုများ  
- **အနည်းဆုံးခွင့်ပြုချက် သဘောတရားကို အသုံးချပါ:** MCP server သည် လုပ်ဆောင်ရန် လိုအပ်သည့် အနည်းဆုံး ခွင့်ပြုချက်များသာ ပေးပါ။ ဤခွင့်ပြုချက်များကို ပုံမှန် ပြန်လည်သုံးသပ်ပြီး လိုအပ်သည့်အတိုင်းသာ ရှိနေစေရန် သေချာစေ
The confused deputy problem သည် MCP server တစ်ခုသည် MCP client များနှင့် third-party API များအကြား proxy အဖြစ် လုပ်ဆောင်သောအခါ ဖြစ်ပေါ်လာနိုင်သည့် လုံခြုံရေးအားနည်းချက်တစ်ခုဖြစ်သည်။ ဤအားနည်းချက်ကို MCP server သည် static client ID ကို third-party authorization server နှင့် authentication ပြုလုပ်ရာတွင် dynamic client registration ကို မထောက်ပံ့သည့် authorization server ကို အသုံးပြုသောအခါ အကျိုးပြုနိုင်သည်။

### အန္တရာယ်များ

- **Cookie-based consent bypass**: အသုံးပြုသူသည် ယခင်က MCP proxy server မှတဆင့် authentication ပြုလုပ်ပြီးသားဖြစ်ပါက၊ third-party authorization server သည် အသုံးပြုသူ၏ browser တွင် consent cookie တစ်ခုကို သတ်မှတ်နိုင်သည်။ အဆိုပါ cookie ကို အသုံးပြု၍ အတုယူသူသည် အသုံးပြုသူအား authorization request ပါဝင်သည့် မကောင်းသော redirect URI ပါသော မကောင်းသောလင့်ခ်တစ်ခု ပေးပို့ကာ အကျိုးပြုနိုင်သည်။
- **Authorization code ခိုးယူခြင်း**: အသုံးပြုသူသည် မကောင်းသောလင့်ခ်ကို နှိပ်သောအခါ၊ third-party authorization server သည် ရှိပြီးသား cookie ကြောင့် consent screen ကို ကျော်လွှားပြီး authorization code ကို အတုယူသူ၏ server သို့ redirect ပြုလုပ်နိုင်သည်။
- **မခွင့်ပြုထားသော API ဝင်ရောက်ခွင့်**: အတုယူသူသည် ခိုးယူထားသော authorization code ကို access token များအဖြစ် လဲလှယ်ကာ အသုံးပြုသူအဖြစ် impersonate ပြုလုပ်၍ third-party API ကို ခွင့်ပြုချက်မရှိဘဲ ဝင်ရောက်နိုင်သည်။

### ကာကွယ်ထိန်းချုပ်မှုများ

- **သေချာသော consent လိုအပ်ချက်များ**: Static client ID များကို အသုံးပြုသည့် MCP proxy server များသည် third-party authorization server များသို့ ပို့ဆောင်မည့်အခါ dynamic client တစ်ခုချင်းစီအတွက် အသုံးပြုသူ၏ သေချာသော consent ကို ရယူရမည်။
- **OAuth ကို မှန်ကန်စွာ အကောင်အထည်ဖော်ခြင်း**: Authorization request များအတွက် code challenges (PKCE) ကို အသုံးပြုခြင်းအပါအဝင် OAuth 2.1 လုံခြုံရေးအကောင်းဆုံး လမ်းညွှန်ချက်များကို လိုက်နာရန်၊ interception အတိုက်ခိုက်မှုများကို ကာကွယ်ရန်။
- **Client အတည်ပြုခြင်း**: မကောင်းသောသူများမှ အကျိုးပြုခြင်းကို ကာကွယ်ရန် redirect URI များနှင့် client identifier များကို တင်းကြပ်စွာ အတည်ပြုရန်။

# Token Passthrough Vulnerabilities

### ပြဿနာအကြောင်းအရာ

"Token passthrough" သည် MCP server တစ်ခုသည် MCP client မှ token များကို MCP server ကိုပေးအပ်ခြင်းမပြုဘဲ တိုက်ရိုက် downstream API များသို့ "ဖြတ်သန်းပေး" သည့် anti-pattern ဖြစ်သည်။ ဤလုပ်ဆောင်ချက်သည် MCP authorization specification ကို ထိရောက်စွာ ချိုးဖောက်ပြီး လုံခြုံရေးအန္တရာယ်များကို ဖြစ်ပေါ်စေသည်။

### အန္တရာယ်များ

- **လုံခြုံရေးထိန်းချုပ်မှုများ ကျော်လွှားခြင်း**: Clients များသည် rate limiting, request validation, traffic monitoring ကဲ့သို့သော လုံခြုံရေးထိန်းချုပ်မှုများကို မမှန်ကန်စွာ စစ်ဆေးခြင်းမရှိဘဲ downstream API များနှင့် တိုက်ရိုက် token များကို အသုံးပြုနိုင်သည်။
- **တာဝန်ယူမှုနှင့် စစ်ဆေးမှု ပြဿနာများ**: MCP server သည် upstream မှ ထုတ်ပေးသော access token များကို အသုံးပြုသော client များကို ခွဲခြားနိုင်ခြင်းမရှိသဖြင့် ဖြစ်ရပ်များ စုံစမ်းစစ်ဆေးခြင်းနှင့် စစ်ဆေးမှုများ ပြုလုပ်ရန် အခက်အခဲ ဖြစ်ပေါ်စေသည်။
- **ဒေတာ ထွက်ပေါက်ခြင်း**: Token များကို မှန်ကန်သော claims validation မပြုဘဲ ဖြတ်သန်းပေးပါက ခိုးယူထားသော token ဖြင့် မကောင်းသောသူတစ်ဦးသည် server ကို proxy အဖြစ် အသုံးပြု၍ ဒေတာ ထွက်ပေါက်မှုများ ဖြစ်ပေါ်စေနိုင်သည်။
- **ယုံကြည်မှုနယ်နိမိတ် ချိုးဖောက်ခြင်း**: Downstream resource server များသည် မူလအရင်းအမြစ် သို့မဟုတ် အပြုအမူ ပုံစံများအပေါ် အခြေခံ၍ ယုံကြည်မှု ပေးသည်။ ယုံကြည်မှုနယ်နိမိတ် ချိုးဖောက်ခြင်းသည် မမျှော်လင့်ထားသော လုံခြုံရေးပြဿနာများ ဖြစ်ပေါ်စေနိုင်သည်။
- **Multi-service Token မမှန်ကန်စွာ အသုံးပြုခြင်း**: Token များကို ဝန်ဆောင်မှုများစွာမှ လက်ခံပြီး မှန်ကန်စွာ စစ်ဆေးခြင်းမရှိပါက ဝန်ဆောင်မှုတစ်ခု ခိုးယူခံရသူသည် အခြား ဝန်ဆောင်မှုများကိုလည်း token ဖြင့် ဝင်ရောက်နိုင်သည်။

### ကာကွယ်ထိန်းချုပ်မှုများ

- **Token validation**: MCP server များသည် MCP server အတွက်သာ ထုတ်ပေးထားသော token များကိုသာ လက်ခံရမည်။
- **Audience verification**: Token များတွင် MCP server ၏ အတည်ပြုချက်နှင့် ကိုက်ညီသော audience claim ရှိကြောင်း အမြဲစစ်ဆေးရမည်။
- **Token lifecycle ကို မှန်ကန်စွာ စီမံခန့်ခွဲခြင်း**: Token ခိုးယူခြင်းနှင့် မမှန်ကန်စွာ အသုံးပြုခြင်း အန္တရာယ်ကို လျော့နည်းစေရန် အချိန်တို access token များနှင့် token rotation ကို မှန်ကန်စွာ အကောင်အထည်ဖော်ရန်။

# Session Hijacking

### ပြဿနာအကြောင်းအရာ

Session hijacking သည် client တစ်ဦးအား server မှ session ID တစ်ခု ပေးပြီး၊ မခွင့်ပြုထားသော တစ်ဦးတစ်ယောက်က ထို session ID ကို ခိုးယူ၍ မူလ client အဖြစ် impersonate ပြုလုပ်ကာ မခွင့်ပြုထားသော လုပ်ဆောင်ချက်များ ပြုလုပ်ခြင်းဖြစ်သည်။ ၎င်းသည် stateful HTTP server များတွင် MCP request များကို ကိုင်တွယ်ရာတွင် အထူးသဖြင့် စိုးရိမ်ရသော အတိုက်ခိုက်နည်းဖြစ်သည်။

### အန္တရာယ်များ

- **Session Hijack Prompt Injection**: Session ID ကို ခိုးယူထားသူသည် client ချိတ်ဆက်ထားသော server နှင့် session state ကို မျှဝေသော server သို့ မကောင်းသော event များ ပို့နိုင်ပြီး အန္တရာယ်ရှိသော လုပ်ဆောင်ချက်များကို ဖြစ်စေခြင်း သို့မဟုတ် အချက်အလက်များကို ဝင်ရောက်ကြည့်ရှုနိုင်သည်။
- **Session Hijack Impersonation**: ခိုးယူထားသော session ID ဖြင့် အတုယူသူသည် MCP server ကို တိုက်ရိုက် ခေါ်ဆိုကာ authentication ကို ကျော်လွှားပြီး တရားဝင်အသုံးပြုသူအဖြစ် ဆက်ဆောင်နိုင်သည်။
- **Compromised Resumable Streams**: Server တစ်ခုသည် redelivery/resumable streams ကို ထောက်ပံ့ပါက အတုယူသူသည် တောင်းဆိုမှုတစ်ခုကို မတော်တဆ ရပ်တန့်စေပြီး မူလ client မှ နောက်ပိုင်းတွင် ပြန်လည်ဆက်လက်လုပ်ဆောင်ရာတွင် မကောင်းသော အကြောင်းအရာများ ပါဝင်နိုင်သည်။

### ကာကွယ်ထိန်းချုပ်မှုများ

- **Authorization verification**: Authorization ကို အကောင်အထည်ဖော်သည့် MCP server များသည် ဝင်ရောက်လာသော တောင်းဆိုမှုအားလုံးကို စစ်ဆေးရမည်ဖြစ်ပြီး session များကို authentication အတွက် အသုံးမပြုရ။
- **Secure session IDs**: MCP server များသည် လုံခြုံပြီး မကြိုတင်ခန့်မှန်းနိုင်သော session ID များကို secure random number generator များဖြင့် ဖန်တီးရမည်။ ခန့်မှန်းနိုင်သော သို့မဟုတ် အဆက်မပြတ် ID များကို ရှောင်ရှားရန်။
- **User-specific session binding**: MCP server များသည် session ID များကို အသုံးပြုသူအထူးသတ်မှတ်ချက်များနှင့် ပေါင်းစပ်၍ `<user_id>:<session_id>` ကဲ့သို့သော ဖော်မတ်ဖြင့် binding ပြုလုပ်သင့်သည်။
- **Session expiration**: Session ID ခိုးယူခံရပါက အန္တရာယ်ကာလကို ကန့်သတ်ရန် session သက်တမ်းကုန်ဆုံးမှုနှင့် rotation ကို မှန်ကန်စွာ အကောင်အထည်ဖော်ရန်။
- **Transport security**: Session ID များ ခိုးယူခံရမှုကို ကာကွယ်ရန် ဆက်သွယ်မှုအားလုံးတွင် HTTPS ကို အမြဲအသုံးပြုရန်။

# Supply chain security

Supply chain security သည် AI ခေတ်တွင် အခြေခံအရေးပါမှုရှိနေဆဲဖြစ်သော်လည်း သင့် supply chain အတွင်း ပါဝင်သည့် အရာများ၏ အကျယ်အဝန်းသည် ကျယ်ပြန့်လာသည်။ ရိုးရာ code package များအပြင် foundation model များ၊ embeddings service များ၊ context provider များနှင့် third-party API များကိုလည်း တိကျစွာ စစ်ဆေးကြည့်ရှုခြင်းနှင့် စောင့်ကြည့်ခြင်း လိုအပ်သည်။ ၎င်းတို့သည် မှန်ကန်စွာ စီမံမထားပါက အားနည်းချက်များ သို့မဟုတ် အန္တရာယ်များ ဖြစ်ပေါ်စေနိုင်သည်။

**AI နှင့် MCP အတွက် အဓိက supply chain security လုပ်ထုံးလုပ်နည်းများ**  
- **ပေါင်းစည်းမှုမပြုမီ အစိတ်အပိုင်းအားလုံးကို စစ်ဆေးရန်**: Open-source library များသာမက AI model များ၊ ဒေတာရင်းမြစ်များနှင့် ပြင်ပ API များကိုပါ စစ်ဆေးရန်။ မူလအရင်းအမြစ်၊ လိုင်စင်နှင့် သိရှိထားသော အားနည်းချက်များကို အမြဲစစ်ဆေးရန်။  
- **လုံခြုံသော deployment pipeline များ ထိန်းသိမ်းရန်**: CI/CD pipeline များတွင် လုံခြုံရေး စစ်ဆေးမှုများကို အလိုအလျောက် ထည့်သွင်းကာ ပြဿနာများကို အစောဆုံး တွေ့ရှိနိုင်ရန်။ ယုံကြည်ရသော artifact များကိုသာ production သို့ ထုတ်ပေးရန်။  
- **ဆက်လက် စောင့်ကြည့်ခြင်းနှင့် စစ်ဆေးခြင်း**: Model များနှင့် ဒေတာဝန်ဆောင်မှုများအပါအဝင် အားလုံးကို ဆက်လက် စောင့်ကြည့်ကာ supply chain အတိုက်ခိုက်မှုများ သို့မဟုတ် အားနည်းချက်အသစ်များကို ရှာဖွေရန်။  
- **အနည်းဆုံးခွင့်ပြုချက်နှင့် ဝင်ရောက်ခွင့် ထိန်းချုပ်မှုများ**: MCP server ၏ လုပ်ဆောင်မှုအတွက် လိုအပ်သည့် အရာများကိုသာ model များ၊ ဒေတာများနှင့် ဝန်ဆောင်မှုများသို့ ဝင်ရောက်ခွင့်ပေးရန် ကန့်သတ်ရန်။  
- **အန္တရာယ်များကို အမြန်တုံ့ပြန်ရန်**: ခိုးယူခံရသည့် အစိတ်အပိုင်းများကို ပြင်ဆင်ခြင်း သို့မဟုတ် အစားထိုးခြင်း၊ လျှို့ဝှက်ချက်များ သို့မဟုတ် အတည်ပြုချက်များကို လှည့်ပြောင်းခြင်း အတွက် လုပ်ထုံးလုပ်နည်းများ ရှိထားရန်။

[GitHub Advanced Security] သည် secret scanning, dependency scanning, CodeQL analysis ကဲ့သို့သော လုပ်ဆောင်ချက်များကို ပံ့ပိုးပေးသည်။ ဤကိရိယာများကို [Azure DevOps] နှင့် [Azure Repos] နှင့် ပေါင်းစည်းကာ ကုဒ်နှင့် AI supply chain အားလုံးတွင် အားနည်းချက်များကို ရှာဖွေကာ ကာကွယ်နိုင်ရန် အကူအညီပေးသည်။

Microsoft သည် ထုတ်ကုန်အားလုံးအတွက် supply chain security လုပ်ထုံးလုပ်နည်းများကို အတွင်းပိုင်းတွင် ကျယ်ပြန့်စွာ အသုံးပြုထားသည်။ ပိုမိုသိရှိလိုပါက [The Journey to Secure the Software Supply Chain at Microsoft] ကို ကြည့်ရှုနိုင်ပါသည်။

# MCP implementation ၏ လုံခြုံရေးအခြေအနေကို မြှင့်တင်ပေးမည့် အတည်ပြုထားသော လုံခြုံရေးအကောင်းဆုံး လုပ်ထုံးလုပ်နည်းများ

MCP implementation တစ်ခုသည် သင့်အဖွဲ့အစည်း၏ ပတ်ဝန်းကျင်ရှိ လုံခြုံရေးအခြေအနေကို ဆက်ခံရရှိသဖြင့် MCP ကို သင့် AI စနစ်များ၏ အစိတ်အပိုင်းတစ်ခုအဖြစ် စဉ်းစားရာတွင် သင့်လုံခြုံရေးအခြေအနေကို မြှင့်တင်ရန် အကြံပြုသည်။ အောက်ပါ အတည်ပြုထားသော လုံခြုံရေးထိန်းချုပ်မှုများမှာ အထူးသဖြင့် သင့်အတွက် သင့်လျော်သည်။

- သင့် AI application တွင် secure coding အကောင်းဆုံး လုပ်ထုံးလုပ်နည်းများ - [OWASP Top 10] နှင့် [OWASP Top 10 for LLMs] အပါအဝင်၊ လျှို့ဝှက်ချက်များနှင့် token များအတွက် secure vault များ အသုံးပြုခြင်း၊ application အစိတ်အပိုင်းအားလုံးအကြား end-to-end လုံခြုံသော ဆက်သွယ်မှုများ အကောင်အထည်ဖော်ခြင်း။
- Server hardening - MFA ကို အသုံးပြုနိုင်သမျှ အသုံးပြုခြင်း၊ patch များကို အမြဲတမ်း update ပြုလုပ်ခြင်း၊ third-party identity provider နှင့် ပေါင်းစည်းခြင်း။
- စက်ပစ္စည်းများ၊ အခြေခံအဆောက်အအုံနှင့် application များကို patch များဖြင့် အမြဲတမ်း update ပြုလုပ်ခြင်း။
- လုံခြုံရေး စောင့်ကြည့်မှု - AI application (MCP client/server များအပါအဝင်) ၏ logging နှင့် monitoring ကို အကောင်အထည်ဖော်ကာ အထူးသဖြင့် anomalous လုပ်ဆောင်ချက်များကို စစ်ဆေးရန် SIEM သို့ logs များ ပို့ခြင်း။
- Zero trust architecture - AI application တစ်ခု ခိုးယူခံရပါက lateral movement ကို လျော့နည်းစေရန် network နှင့် identity ထိန်းချုပ်မှုများဖြင့် component များကို သီးခြားထားခြင်း။

# အဓိက သင်ခန်းစာများ

- လုံခြုံရေး အခြေခံများသည် အရေးကြီးနေဆဲဖြစ်သည်။ Secure coding, least privilege, supply chain verification နှင့် ဆက်လက် စောင့်ကြည့်မှုများသည် MCP နှင့် AI workload များအတွက် မရှိမဖြစ် လိုအပ်သည်။
- MCP သည် prompt injection, tool poisoning, session hijacking, confused deputy problem, token passthrough vulnerabilities နှင့် အလွန်အမင်းခွင့်ပြုချက်များကဲ့သို့သော အန္တရာယ်အသစ်များကို မိတ်ဆက်ပေးပြီး ယင်းတို့အတွက် ရိုးရာနှင့် AI အထူးထိန်းချုပ်မှုများ လိုအပ်သည်။
- Microsoft Entra ID ကဲ့သို့သော ပြင်ပ identity provider များကို အသုံးပြုကာ authentication, authorization နှင့် token management ကို ခိုင်မာစွာ ဆောင်ရွက်ရန်။
- Indirect prompt injection နှင့် tool poisoning ကို ကာကွယ်ရန် tool metadata ကို စစ်ဆေးခြင်း၊ dynamic ပြောင်းလဲမှုများကို စောင့်ကြည့်ခြင်းနှင့် Microsoft Prompt Shields ကဲ့သို့သော ဖြေရှင်းနည်းများကို အသုံးပြုရန်။
- Non-deterministic session ID များကို အသုံးပြုခြင်း၊ session များကို user identity နှင့် binding ပြုလုပ်ခြင်းနှင့် authentication အတွက် session မသုံးရန် secure session management ကို အကောင်အထည်ဖော်ရန်။
- Confused deputy attacks မဖြစ်ပေါ်စေရန် dynamic client တစ်ခုချင်းစီအတွက် အသုံးပြုသူ၏ သေချာသော consent ကို လိုအပ်သည့်အတိုင်း ရယူခြင်းနှင့် OAuth လုံခြုံရေး လုပ်ထုံးလုပ်နည်းများကို မှန်ကန်စွာ လိုက်နာရန်။
- Token passthrough vulnerabilities မဖြစ်ပေါ်

**အကြောင်းကြားချက်**  
ဤစာတမ်းကို AI ဘာသာပြန်ဝန်ဆောင်မှု [Co-op Translator](https://github.com/Azure/co-op-translator) ဖြင့် ဘာသာပြန်ထားပါသည်။ ကျွန်ုပ်တို့သည် တိကျမှန်ကန်မှုအတွက် ကြိုးစားသော်လည်း အလိုအလျောက် ဘာသာပြန်ခြင်းတွင် အမှားများ သို့မဟုတ် မှားယွင်းချက်များ ပါဝင်နိုင်ကြောင်း သတိပြုပါရန် မေတ္တာရပ်ခံအပ်ပါသည်။ မူရင်းစာတမ်းကို မိမိဘာသာစကားဖြင့်သာ တရားဝင်အချက်အလက်အဖြစ် ယူဆသင့်ပါသည်။ အရေးကြီးသော အချက်အလက်များအတွက် လူ့ပညာရှင်များ၏ ပရော်ဖက်ရှင်နယ် ဘာသာပြန်ခြင်းကို အကြံပြုပါသည်။ ဤဘာသာပြန်ချက်ကို အသုံးပြုရာမှ ဖြစ်ပေါ်လာနိုင်သည့် နားလည်မှုမှားယွင်းမှုများအတွက် ကျွန်ုပ်တို့သည် တာဝန်မခံပါ။