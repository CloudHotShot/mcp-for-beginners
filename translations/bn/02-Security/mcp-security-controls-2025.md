<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "b59b477037dc1dd6b1740a0420f3be14",
  "translation_date": "2025-07-17T01:49:32+00:00",
  "source_file": "02-Security/mcp-security-controls-2025.md",
  "language_code": "bn"
}
-->
# সর্বশেষ MCP সিকিউরিটি কন্ট্রোলস - জুলাই ২০২৫ আপডেট

মডেল কনটেক্সট প্রোটোকল (MCP) যেমন বিকশিত হচ্ছে, নিরাপত্তা একটি গুরুত্বপূর্ণ বিবেচ্য বিষয় হিসেবে রয়ে গেছে। এই ডকুমেন্টে জুলাই ২০২৫ পর্যন্ত MCP নিরাপদে বাস্তবায়নের জন্য সর্বশেষ সিকিউরিটি কন্ট্রোলস এবং সেরা অনুশীলনগুলি তুলে ধরা হয়েছে।

## প্রমাণীকরণ এবং অনুমোদন

### OAuth 2.0 ডেলিগেশন সাপোর্ট

MCP স্পেসিফিকেশনের সাম্প্রতিক আপডেটগুলো MCP সার্ভারগুলোকে ব্যবহারকারীর প্রমাণীকরণ Microsoft Entra ID-এর মতো বাহ্যিক সার্ভিসে ডেলিগেট করার সুযোগ দেয়। এটি নিরাপত্তার দিক থেকে উল্লেখযোগ্য উন্নতি আনে:

1. **কাস্টম অথ ইমপ্লিমেন্টেশন বাদ দেওয়া**: কাস্টম অথ কোডে নিরাপত্তা ত্রুটির ঝুঁকি কমায়  
2. **প্রতিষ্ঠিত আইডেন্টিটি প্রোভাইডার ব্যবহার**: এন্টারপ্রাইজ-গ্রেড নিরাপত্তা সুবিধা গ্রহণ  
3. **আইডেন্টিটি ম্যানেজমেন্ট কেন্দ্রীকরণ**: ব্যবহারকারীর জীবনচক্র এবং অ্যাক্সেস নিয়ন্ত্রণ সহজতর করে  

## টোকেন পাসথ্রু প্রতিরোধ

MCP অনুমোদন স্পেসিফিকেশন স্পষ্টভাবে টোকেন পাসথ্রু নিষিদ্ধ করে যাতে নিরাপত্তা নিয়ন্ত্রণ এড়ানো এবং দায়িত্ব এড়ানোর সমস্যা না হয়।

### প্রধান প্রয়োজনীয়তা

1. **MCP সার্ভারগুলো তাদের জন্য ইস্যুকৃত নয় এমন টোকেন গ্রহণ করবে না**: নিশ্চিত করুন সব টোকেনের audience claim সঠিক  
2. **সঠিক টোকেন যাচাই প্রয়োগ করুন**: issuer, audience, মেয়াদ উত্তীর্ণ হওয়া, এবং সিগনেচার পরীক্ষা করুন  
3. **আলাদা টোকেন ইস্যু করুন**: বিদ্যমান টোকেন পাস না করে ডাউনস্ট্রিম সার্ভিসের জন্য নতুন টোকেন ইস্যু করুন  

## নিরাপদ সেশন ম্যানেজমেন্ট

সেশন হাইজ্যাকিং এবং ফিক্সেশন আক্রমণ প্রতিরোধে নিম্নলিখিত নিয়ন্ত্রণগুলি প্রয়োগ করুন:

1. **নিরাপদ, অপ্রেডিক্টেবল সেশন আইডি ব্যবহার করুন**: ক্রিপ্টোগ্রাফিক্যালি সিকিউর র‍্যান্ডম নাম্বার জেনারেটর দিয়ে তৈরি  
2. **সেশনগুলো ব্যবহারকারীর পরিচয়ের সাথে বেঁধে দিন**: সেশন আইডি ব্যবহারকারী-নির্দিষ্ট তথ্যের সাথে মিলিয়ে রাখুন  
3. **সঠিক সেশন রোটেশন প্রয়োগ করুন**: প্রমাণীকরণ পরিবর্তন বা প্রিভিলেজ বৃদ্ধির পর  
4. **উপযুক্ত সেশন টাইমআউট সেট করুন**: নিরাপত্তা এবং ব্যবহারকারীর অভিজ্ঞতার মধ্যে সঠিক ভারসাম্য বজায় রাখুন  

## টুল এক্সিকিউশন স্যান্ডবক্সিং

ল্যাটারাল মুভমেন্ট প্রতিরোধ এবং সম্ভাব্য কম্প্রোমাইজ সীমাবদ্ধ করতে:

1. **টুল এক্সিকিউশন এনভায়রনমেন্ট আলাদা করুন**: কন্টেইনার বা আলাদা প্রসেস ব্যবহার করুন  
2. **রিসোর্স লিমিট প্রয়োগ করুন**: রিসোর্স এক্সহস্টশন আক্রমণ প্রতিরোধে  
3. **ন্যূনতম প্রিভিলেজ অ্যাক্সেস দিন**: শুধুমাত্র প্রয়োজনীয় অনুমতি প্রদান করুন  
4. **এক্সিকিউশন প্যাটার্ন মনিটর করুন**: অস্বাভাবিক আচরণ শনাক্ত করতে  

## টুল ডেফিনিশন সুরক্ষা

টুল পয়জনিং প্রতিরোধে:

1. **ব্যবহারের আগে টুল ডেফিনিশন যাচাই করুন**: ক্ষতিকারক নির্দেশনা বা অনুপযুক্ত প্যাটার্ন খুঁজে বের করুন  
2. **ইন্টিগ্রিটি যাচাই ব্যবহার করুন**: টুল ডেফিনিশনের হ্যাশ বা সিগনেচার করে অননুমোদিত পরিবর্তন শনাক্ত করুন  
3. **পরিবর্তন মনিটরিং প্রয়োগ করুন**: টুল মেটাডেটার অপ্রত্যাশিত পরিবর্তনে সতর্কতা দিন  
4. **টুল ডেফিনিশনের ভার্সন কন্ট্রোল করুন**: পরিবর্তন ট্র্যাক করুন এবং প্রয়োজনে রোলব্যাক সক্ষম করুন  

এই নিয়ন্ত্রণগুলো একসাথে কাজ করে MCP বাস্তবায়নের জন্য একটি শক্তিশালী নিরাপত্তা অবকাঠামো তৈরি করে, যা AI-চালিত সিস্টেমের অনন্য চ্যালেঞ্জ মোকাবেলা করে এবং শক্তিশালী প্রচলিত নিরাপত্তা অনুশীলন বজায় রাখে।

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ সেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনূদিত হয়েছে। আমরা যথাসাধ্য সঠিকতার চেষ্টা করি, তবে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। মূল নথিটি তার নিজস্ব ভাষায়ই কর্তৃত্বপূর্ণ উৎস হিসেবে বিবেচিত হওয়া উচিত। গুরুত্বপূর্ণ তথ্যের জন্য পেশাদার মানব অনুবাদ গ্রহণ করার পরামর্শ দেওয়া হয়। এই অনুবাদের ব্যবহারে সৃষ্ট কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যার জন্য আমরা দায়ী নই।