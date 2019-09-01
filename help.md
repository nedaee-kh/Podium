میتوانیم فهرست مطالب داشته باشیم:

- [نحوه درست کردن Tab](#%d9%86%d8%ad%d9%88%d9%87-%d8%af%d8%b1%d8%b3%d8%aa-%da%a9%d8%b1%d8%af%d9%86-tab)
- [نتیجه گیری](#%d9%86%d8%aa%db%8c%d8%ac%d9%87-%da%af%db%8c%d8%b1%db%8c)

## نحوه درست کردن Tab


می‌تونیم تب‌ باکس‌های متعددی داشته باشیم.

<div class="tab-start">
</div>


# [JavaScript](#tab/javascript)


``` javascript

let a = parseInt("10");


```

<div class="swaggerLink">http://docs.pod.land/v1.0.8.0/Developer/User/152/AccessToken</div>

# [C#](#tab/csharp)

``` csharp

int a = int.Parse("10");


```

<div class="swaggerLink">http://swagger-tab2-csharp.com</div>




<div class="tab-end">
</div>


- [بن شارژ اعتبار](#couponCharge)
- [بن تخفیف مبلغی](#%D8%A8%D9%86-%D8%AA%D8%AE%D9%81%DB%8C%D9%81-%D9%85%D8%A8%D9%84%D8%BA%DB%8C)
- [بن تخفیف درصدی](#couponPercent)
- [اعمال ووچر به فاکتور](#couponVoucherToBill)
- [دریافت و جستجو لیست بن‌ها](#couponList)
- [فعالسازی و غیرفعالسازی بن تخفیف](#couponActivation)

## بن تخفیف

با استفاده از سرویس‌های مربوط به تخفیف پاد، شما می توانید برای استفاده از خدما‌تتان برای همه یا برخی از کاربر‌انتان تخفیف اعمال کنید و یا به آن‌ها کد‌های تخفیف بدهید.

## بن شارژ اعتبار {#couponCharge}

جهت تعریف شارژ اعتبار، سرویس زیر را فراخوانی نمایید:

```
Header:
	_token_=[api_token]
	_token_issuer_=1
Method:  GET 
URL:
        [platform-address]/nzh/biz/defineCreditVoucher
Parameters:
        // برای ملاحظه پارامترها به لینک"تست و نمونه کد" مراجعه نمایید
```


توجه داشته باشید به ازای هر بن تخفیف، باید مقادیر تعداد، مبلغ، نام و توضیحات در پارامترهای جداگانه ارسال گردند.

## بن تخفیف مبلغی 

برای ساخت بن تخفیف با مبلغ مشخص، سرویس زیر را فراخوانی نمایید؛ می‌توانید با یک بار فراخوانی سرویس، برای چند کاربر اعتبار تعریف نمایید، اما توجه داشته باشید به ازای هر کاربر، کد هش متفاوتی دریافت خواهید کرد و مشتری با اعمال کد هش می‌تواند از شارژ تعریف شده استفاده نماید.

جهت تعریف شارژ، لازم است در صنف خود حتما اعتبار داشته باشید، هم‌چنین می‌توانید کد هش را به صورت دلخواه تعریف نمایید.

```
Header:
	_token_=[api_token]
	_token_issuer_=1
Method:  GET 
URL:
        [platform-address]/nzh/biz/defineDiscountAmountVoucher
Parameters:
        // برای ملاحظه پارامترها به لینک"تست و نمونه کد" مراجعه نمایید
```


توجه داشته باشید به ازای هر بن تخفیف، باید مقادیر تعداد، مبلغ، نام و توضیحات در پارامترهای جداگانه ارسال گردند.

## بن تخفیف درصدی {#couponPercent}

جهت تعریف شارژ بن تخفیف، در قالب درصد سرویس ذیل را فراخوانی نمایید:

```
Header:
	_token_=[api_token]
	_token_issuer_=1
Method:  GET 
URL:
        [platform-address]/nzh/biz/defineDiscountPercentageVoucher
Parameters:
        // برای ملاحظه پارامترها به لینک"تست و نمونه کد" مراجعه نمایید
```


توجه داشته باشید به ازای هر بن تخفیف، باید مقادیر تعداد، درصد، نام و توضیحات در پارامترهای جداگانه ارسال گردند.

در صورت تعیین سقف مبلغ برای بن درصدی، در صورتی که بن بیش از یکبار قابل استفاده باشد، در دفعات بعدی مبلغ باقیمانده نسبت به سقف تعیین شده، قابل استفاده است.

در تعریف بن تخفیف درصدی **GuildCode** بعنوان حوزه ی مصرف بن اجباری است.

"guildCode":  نام صنف مطابق با صنف موجود در پنل می‌باشد.

## اعمال ووچر به فاکتور {#couponVoucherToBill}

بعد از تعریف ووچر، برای اعمال ووچر به فاکتور (درصورتی که پارامتر postVoucherEnabled در صدور فاکتور را با مقدار true ارسال نموده باشید)، سرویس ذیل را فراخوانی نمایید:

```
Header:
	_token_=[api_token]
	_token_issuer_=1
        _ott_=[one time token]
Method:  GET 
URL:
        [platform-address]/nzh/biz/applyVoucher
Parameters:
        invoiceId= 
        voucherHash= // لیست کد بن تخفیف
        preview=[true/false] // پیش نمایش اعمال ووچر روی فاکتور - در سیستم ثبت نمی‌گردد
```


بن تخفیف جهت اعمال روی یک فاکتور، می‌تواند بیش از یک مورد باشد.

## دریافت و جستجو لیست بن‌ها {#couponList}

با سرویس زیر امکان خواهید داشت در بین لیست‌های بن کسب و کارتان جستجو و آن را دریافت نمایید:

```
Header:
	_token_=[api_token]
	_token_issuer_=1
Method:  GET 
URL:
        [platform-address]/nzh/biz/getVoucherList
Parameters:
        // برای ملاحظه پارامترها به لینک"تست و نمونه کد" مراجعه نمایید
```


توجه داشته باشید به ازای هر بن تخفیف، باید مقادیر تعداد، مبلغ، نام و توضیحات در پارامترهای جداگانه ارسال گردند.

## فعالسازی و غیرفعالسازی بن تخفیف {#couponActivation}

سرویس ذیل را جهت غیرفعال کردن بن تخفیف زودتر از موعد فراخوانی نمایید:

```
Header:
	_token_=[api_token]
	_token_issuer_=1
Method:  GET 
URL:
        [platform-address]/nzh/biz/deactivateVoucher
Parameters:
        id=
```


فعال نمودن مجدد بن تخفیف:

```
Header:
	_token_=[api_token]
	_token_issuer_=1
Method:  GET 
URL:
        [platform-address]/nzh/biz/activateVoucher
Parameters:
        id=
```



## نتیجه گیری
