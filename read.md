# گردشگری
در زمینه گردشگری کسب و کارهای مختلفی و در حوزه‌های مختلفی مشغول به فعالیت هستند. بعنوان مثال کسب و کارهایی با محوریت فروش بلیط هواپیما، اتوبوس یا قطار و یا اجاره مکان‌هایی برای اقامت، معرفی مکان‌های گردشگری و ...اگر کسب و کار آنلاین شما هم به نوعی با گردشگری مربوط است، این مستند برای شما مفید خواهد بود.

<div class="box-end">
</div>

## محتوای سفارشی
یکی از بهترین اقدامات در جهت جذب گردشگران، تبلیغ در مورد مکان‌های دیدنی در شبکه‌های اجتماعی و یا وبسایت‌ها است. با استفاده از این سرویس شما می‌توانید با امکان کامنت‌گذاری، از افرادی که از آن مکان دیدن کردند بخواهید تا نظراتشان را با سایرین به اشتراک بگذارند.

### ایجاد و دریافت پست سفارشی 
پست سفارشی پستی است که محتوای متنی دارد. می توان از metadata این نوع پست که به صورت json ذخیره میگردد برای تامین نیازهای خاص کسب و کار استفاده نمود.

    HEADER:
            _token_=[API_TOKEN]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/addCustomPost/
    Parameters:
            name=[The Name of Post]
            canComment=[true/false]
            canLike=[true/false]
            content=[The Content of Post]
            enable=[true/false]		امکان دیده شدن پست در تایم لاین کسب و کار توسط مشتریان
            metadata=[A json string to store extra content]
            tags=[STRING: tags separated by ,]
            uniqueId=                // جهت جلوگیری از ثبت مجدد یک پست تکراری می توانید از این فیلد استفاده نمایید
لیست پست‌ها را با سرویس زیر دریافت نمایید. در صورت ارسال activityInfo با مقدار false فقط اطلاعات خود پست برگردانده شده و فعالیت هایی که روی پست  انجام گرفته حذف میشوند.

       HEADER:
            _token_=[API_TOKEN] یا [ACCESS_TOKEN]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/customPostList/
    Parameters:
            businessId=*
            activityInfo=             //default: true; return activities information on post
            id=entityd لیست شناسه موجودیت پست
            categoryCode= لیست کدهای دسته بندی
            firstId=
            lastId=
            offset=0 *
            size=10 *
            tags=  لیست تگ
            tagTrees=  لیست درخت تگ
            uniqueId=                  // استعلام با شناسه ی یکتا  که در سرویس ثبت ارسال شده

 هم‌چنین کاربران نیز امکان گذاشتن پست از طریق سرویس زیر را دارند:
            
             HEADER:
            _token_=[ACCESS_TOKEN]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/addUserPost/
    Parameters:
            name=[The Name of Post]*
            content=[The Content of Post]*
            canComment=[true/false]*
            canLike=[true/false]*
            enable=[true/false]		امکان دیده شدن پست در تایم لاین کسب و کار توسط مشتریان
            lat= محل جغرافیایی آیتم
            lng= محل جغرافیایی آیتم
            tags=[STRING: tags separated by ,]

سپس پست ایجاد شده را می‌توانید در سرویس زیر دریافت نمایید:
       

         HEADER:
            _token_=[ACCESS_TOKEN]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/loadPost/
    Parameters:
            id=entityId *  مقدار شناسه موجودیت پست 

### ارسال پست دسته ای 

   توسط این سرویس قادر خواهید بود تعداد نامحدود پست سفارشی را در یک درخواست ارسال نمایید
```
HEADER:
        _token_=[ api_token ]
        _token_issuer_= 1
Method: POST
Url:
        [platform-address]/nzh/biz/addCustomPostList
Parameters:
       data = [JSON Format]  *
```

   جهت ارسال مقادیر مورد نظر در پارامتر Data سرویس فوق باید به فرمتی که در بخش زیر توضیح داده شده است مقادیر را ارسال کنید.

```
[{
	"name": "Your 1nd Post Name value",
	"content": "Your 1nd Post content value",
	"canComment": "true / false",
	"canLike": "true /false",
	"enable": "true /false",
	"metadata": "{\"Your JSON Key\":\"Your JSON Value\"}",
	"lat": "",
	"lng": "",
	"tags": "tags1,tags2,tags3,....",
	"tagtrees": "Value",
	"tagTreeCategoryName": "Value"
}, {
	"name": "Your 2nd Post Name value",
	"content": "Your 2nd Post content value",
	"canComment": "true / false",
	"canLike": "true /false",
	"enable": "true /false",
	"metadata": "{\"Your JSON Key\":\"Your JSON Value\"}",
	"lat": "",
	"lng": "",
	"tags": "tags1,tags2,tags3,....",
	"tagtrees": "Value",
	"tagTreeCategoryName": ""
}, {
	"name": "Your 3nd Post Name value",
	"content": "Your 3nd Post content value",
	"canComment": "true / false",
	"canLike": "true /false",
	"enable": "true /false",
	"metadata": "{\"Your JSON Key\":\"Your JSON Value\"}",
	"lat": "",
	"lng": "",
	"tags": "tags1,tags2,tags3,....",
	"tagtrees": "Value",
	"tagTreeCategoryName": "Value"

}]
```

تعداد مقادیری که در بالا توضیح داده شده است تا هر مقدار که مایل باشید قابل اضافه شدن میباشد

### ویرایش پست سفارشی 
   جهت ویرایش پست سفارشی ثبت شده توسط کسب و کار، با استفاده از سرویس زیر آن را ویرایش نمایید:

            ```HEADER
	_token_=[API_TOKEN]
	_token_issuer_=1
	Method:
        GET
        Url:
        [platform-address]/nzh/biz/updateCustomPost/ Parameters:
        entityId=[The entity id of post]
        name=[The Name of Post]
        canComment=[true/false]
        canLike=[true/false]
        content=[The Content of Post]
        enable=[true/false]		امکان دیده شدن پست در تایم لاین کسب و کار توسط مشتریان
        metadata=[A json string to store extra content]
        tags=[STRING: tags separated by ,]
        version= // در صورت ارسال این مقدار، باید با ورژن فعلی محصول یکسان باشد

 جهت ویرایش پست سفارشی ثبت شده توسط کاربر، سرویس زیر را فراخوانی نمایید:

    HEADER
    	_token_=[ACCESS_TOKEN]
    	_token_issuer_=1
    Method:
            GET
    Url:
            [platform-address]/nzh/updateUserPost/
    Parameters:
            entityId=[The entity id of post]*
            name=[The Name of Post]*
            content=[The Content of Post]*
            canComment=[true/false]*
            canLike=[true/false]*
            enable=[true/false]*   امکان دیده شدن پست در تایم لاین کسب و کار توسط مشتریان
            tags=[STRING: tags separated by ,]

### کامنت برای محتوا 
       مشتریان شما می توانند برای محتواهایی که شما مجاز نموده اید، کامنت بگذارند. برای این منظور api زیر را با توکن کاربر استفاده 
نمایید.

    HEADER
    	_token_=[ACCESS_TOKEN]
    	_token_issuer_=1
    Method:
            GET 
    Url:
            [platform-address]/nzh/comment/
    Parameters:
            postId=[postId]			this is provided in “userPostInfo” of entity
            comment=[your customer comment]
     

### تایید کامنت برای نمایش به عموم و لغو تایید
از سرویس ذیل برای دریافت تمامی نظرات ثبت شده(تایید شده و تایید نشده)،  استفاده نمایید. هم چنین توکن کسب و کار را در هدر قرار دهید.


    HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
    	GET
    Url:
    	[platform-address]/nzh/biz/commentList
    Parameters:
    	postId= [the id of post]*
    	offset= [offset of pagination]*
    	size= [size of pagination]*
کامنت ها به صورت پیشفرض تایید نشده هستند و بجز برای کسب و کار و خود فرد  نظردهنده نمایش داده نمی شوند. جهت تایید کامنت، نیازمند شناسه کامنت می  باشید، لذا با فراخوانی سرویس دریافت لیست کلی نظرات روی یک پست، لیست  تمامی نظرات را دریافت نموده و کامنت های دلخواه را با  سرویس زیر تایید  نمایید:


    HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
            GET
    Url:
            [platform-address]/nzh/biz/confirmComment/
    Parameters:
            commentId=[The id of Comment]*

و با فراخوانی سرویس ذیل می‌توانید تایید کامنت را لغو نمایید:

       HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
            GET
    Url:
            [platform-address]/nzh/biz/unconfirmComment/
    Parameters:
            commentId=[The id of Comment]*
         

### دریافت کامنتهای یک محتوا 
کامنت هایی که برای یک پست گذاشته شده اند از طریق سرویس زیر دریافت می  شوند. کامنت هایی که از طرف کسب و کار تایید (confirm) نشده باشد فقط به  کاربری که کامنت را ثبت کرده برگردانده می شود.

    HEADER
    	_token_=[ACCESS_TOKEN]
    	_token_issuer_=1
    Method:
            GET
    Url:
            [platform-address]/nzh/commentList/
    Parameters:
            offset=[offset from start of list]
            size=[count of requested comments]
            postId=[postId] 		this is provided in “userPostInfo” of entity


### لایک و دیس‌لایک محتوا 
با استفاده از سرویس زیر میتوانید یک پست را لایک نمایید یا لایک خود را  بردارید. توجه داشته باشید که توکن موجود در هدر شخص لایک کننده را مشخص  مینماید.

    HEADER
    	_token_=[ACCESS_TOKEN]
    	_token_issuer_=1
    Method:
            GET 
    Url:
            [platform-address]/nzh/like/
    Parameters:
            postId=[the postId]*
            dislike=[true/false]	لغو لایک
            

با سرویس زیر می‌توانید یک پست را دیس لایک نمایید:
            
    HEADER
    	_token_=[ACCESS_TOKEN]
    	_token_issuer_=1
    Method:
            GET 
    Url:
            [platform-address]/nzh/dislikePost
    Parameters:
            postId=[the postId] *
            dislike=[true/false]	//  false : مقدار دیفالت برابر است با

### دریافت لیست لایک های یک پست 

با استفاده از این سرویس لیست لایک های یک پست را می توان دریافت نمود:

                HEADER
    	_token_=[ACCESS_TOKEN]
    	_token_issuer_=1
    Method:
            GET
    Url:
            [platform-address]/nzh/likeList/
    Parameters:
            postId=[the entityId of post to view likes]*
            size=[count of requested list]*
            firstId=[first id of result list]
            lastId=[last id of result list]
            offset=[offset count of result list]
   
### لایک کامنت و لیست آن 
با توجه به اینکه می توان برای انواع محتوا، نظر کاربران را دریافت و ثبت  نمود، امکان ثبت علاقه مندی به ازای هر نظر از طرف کاربران دیگر نیز وجود  دارد. از طریق سرویس زیر که با توکن دسترسی کاربر لاگین شده فراخوانی می  شود، کاربر میتواند یک کامنت دیگر را لایک نماید:

    HEADER
    	_token_=[access_token]
    	_token_issuer_=1
    Method:
    	POST
    Url:
    	[platform-address]/nzh/likeComment
    Parameters:
    	commentId= [the id of comment]*
    	dislike= true/fals
   
   اگر پارامتر **dislike** ارسال نشود یا **false** باشد، پست **like** می شود و اگر **true** باشد، لایک آن برداشته می شود.

برای دریافت لیست لایک های یک نظر باز هم با توکن دسترسی کاربر از سرویس زیر استفاده نمایید

    HEADER
    	_token_=[access_token]
    	_token_issuer_=1
    Method:
    	GET
    Url:
    	[platform-address]/nzh/commentLikeList
    Parameters:
    	commentId= [the id of comment]*
    	size= [pagination size]*
            offset= [pagination offset]*
            
        

### دریافت تایم لاین
تایم لاین شامل تمام فعالیت های ارائه شده از سوی کسب و کار به ترتیب زمان است. برای دریافت تایم لاین در کاربردهای مدیریتی کسب و کارتان از api زیر  استفاده نمایید:

         HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
            GET
    Url:
            [platform-address]/nzh/biz/timeline/
    Parameters:
            size=[requsted count of results] *	پارامتر صفحه بندی
            offset=[offset from start of result list] 	پارامتر صفحه بندی 
            firstId=[first id of result list]		 پارامتر صفحه بندی
            type=[typeId]
            entityId=[entityId]
            timelineId=[timelineId]
            tags=[list of required tags separated by ,]
   
   توصیه می شود برای نمایش اطلاعات تایم لاین به مشتریان خود از api زیر با  توکن خود کاربر استفاده نمایید. در این صورت کاربران مواردی که مواردی که enable=false دارند را دریافت نمی کنند و عملیات آن ها قابل پیگیری می شود.

    HEADER
    	_token_=[ACCESS_TOKEN]
    	_token_issuer_=1
    Method:
            GET 
    Url:
            [platform-address]/nzh/timeline/
    Parameters:
            size=[requsted count of results] *	پارامتر صفحه بندی
            offset=[offset from start of result list] 	پارامتر صفحه بندی 
            firstId=[first id of result list]		 پارامتر صفحه بندی
            type=[typeId]
            entityId=[entityId]
            timelineId=[timelineId]
            businessId=[Your business id]

### جستجوی متادیتا 
 در صورتی که پست های سفارشی شما دارای متادیتا باشند، به وسیله سرویس زیر  می توانید آنها را جستجو نمایید. این سرویس پست هایی که متادیتای آنها در  این شرایط صدق می کند را برمی گرداند.
 

    HEADER:
        _token_
        _token_issuer_
    Method:
        POST
    Url:
        [platform-address]/nzh/biz/searchTimelineByMetadata/
    parameters:
        size=[pagination size]
        offset=[pagination offset]
        userId=[userId]                در صورت ارسال، مقادیر تایم لاین با توجه به کاربر ارسالی پر خواهد شد
        type=[code type of entity]   طبق جدول زیر
        metaQuery=[json-query]*    کوئری در فرمت  جیسان که بر متادیتاها اعمال می شود
        orderBy=[fieldName]:[visitCount]:[likeCount]:[commentCount]:[postDate]:[asc|desc] مرتب سازی نتیجه - میتوانید با تکرار این پارامتر بر اساس چندین فیلد مرتب سازی نمایید 
به عنوان metaQuery در درخواست بالا، باید یک آبجکت json ارسال شود که مشخص می کند جستجو بر روی کدام field در متادیتا انجام شود و مقایسه مقدار آن  فیلد توسط چه عملگری انجام شود.
و metaQuery میتواند شامل فیلدهای زیر باشد:  

    {
        "field"    ->  فیلد مورد جستجو در متادیتا
        "is"       ->   برابر بودن مقدار فیلد
        "has"     ->   شامل بودن 
        "gt"       ->   بزرگتر از
        "gte"      ->  بزرگتر مساوی
        "lt"        ->  کوچکتر از
        "lte"      ->  کوچکتر مساوی
    
        "and"     ->  می شوند  AND  می تواند حاوی لیستی از شرط ها باشد که با شرط جاری
        "or"       ->  می شوند  OR  می تواند حاوی لیستی از شرط ها باشد که با شرط جاری
        "not"      ->  می شوند  NOT  می تواند حاوی لیستی از شرط ها باشد که با شرط جاری
 
عمگرهای is و has باید تنهایی استفاده شوند ولی عملگرهای lt / lte و gt / gte می توانند با یگدیگر برای مشخص کردن یک بازه عددی مورد استفاده قرار گیرند.
یک نمونه از آبجکت metaQuery را در زیر میبینید. مثال زیر رکوردهایی که نام آنها دقیقا ali و یا شامل test است به شرطی که سن آنها بین 18 تا 20  یا  بزرگتر از 30 (بجز 33) باشد را بر می گرداند.

    {
    
          "field":"name",
          "is":"ali",
          "or":[
            {
              "field":"name",
              "has":"test"
            }
          ],
          "and":[
            {
              "field":"age",
              "gt":18,
              "lte":20,
              "or":[
                {
                  "field":"age",
                  "gte":30
                }
              ],
              "not":[
                {
                  "field":"age",
                  "is":33
                }
              ]
            }
          ]
        }

چنانچه نیاز به جستجو بر اساس فیلدهای خارج از متادیتا دارید میتوانید از مقدار **item.filedname_**  استفاده نمایید.

به مثال زیر توجه فرمایید

    {
    	"field": "_item.content",
    	"is": "ali",
    	"or": [{
    		"field": "_item.enable",
    		"is": "true"
    	}]
    }

 موارد بالا برای مرتب سازی نیر صدق میکند و میتوانید جهت مرتب سازی نیز از همین روش استفاده نمایید
 
###  جستجوی کامل متنی
   جهت جستجوی کامل در تمام انواع محتوا، از سرویس زیر استفاده نمایید. این سرویس رشته ای از کاراکترها را به عنوان query دریافت نموده و در صورت پیدا کردن آن در هر قسمتی از محتوای خواسته شده، آن را برمی گرداند. همچنین  قابلیت جستجو در محتواهای ثبت شده در بازه زمانی خاص را نیز دارد.
   سرویس زیر با توکن کسب و کار قابل فراخوانی است و تمام محتوای ثبت شده توسط آن کسب و کار را جستجو نموده و موارد غیر فعال را نیز برمی گرداند.
  

     HEADER:
            _token_=[api_token]
            _token_issuer_=1
    Method: POST
    Url:
            [platform-address]/nzh/biz/search
    Parameters:
            query= [string to search] *
            type= [TYPE_ID below]
            guildCodes= [GUILD_CODE]
            tags= [list of tags seperated by , ]
            tagTrees= [list of tag trees seperated by , ]
            dateFrom= [lower limit of creation date ]
            dateTo= [upper limit of creation date ]
            lat=
            lng=
            distance=
            size= [size of pagination] *
            offset= [offset of pagination] *

### بارگذاری تصاویر 
برای بارگذاری تصاویر در پلتفرم و استفاده از لینک آن در ثبت محصول یا اخبار می توانید از apiهای زیر استفاده نمایید:
       

         HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
           POST
    Url: 
           [file-server-address]/nzh/uploadImage/
    Parametrs:
           fileName=[a name for the image]*
           image=[FILE: the image file]*
           xC=&yC=&hC=&wC=[crop of image]


   مقادیر برش تصویر

در صورتی که در سرور سندباکس در حال تست هستید از آدرس

http://sandbox.pod.land:8080

و در صورتی که میخواهید دستورات را در سرور اصلی اجرا نمایید، از آدرس:

https://core.pod.land

به عنوان file-server-address استفاده نمایید.

در پاسخ این درخواست اطلاعات تصویر آپلود شده را دریافت می نمایید:

    {
    	"hasError": false,
    	"errorCode": 0,
    	"count": 0,
    	"ott": "cb0a410ad620474f",
    	"result": 
    	{
    		"id": 544,		 this is the imageId
    		"name": "test",
    		"hashCode": "15d6924edae-0.5464798641551049",
    		"actualWidth": 120,
    		"actualHeight": 120,
    		"width": 400,
    		"height": 300
    	}
    }

برای دریافت مجدد عکس آدرس زیر را بسازید و آن را دریافت نمایید:
        

        GET [file-server-address]/nzh/image/
    ?imageId=[The imageId]*
    &width=[required width to get]             تصویر به این سایز تبدیل و سپس دریافت میشود
    &height=[required height to get]
    &actual=[true/false]			         دریافت تصویر بدون کراپ اعمال شده در مرحله آپلود
    &downloadable=[true/false]	               	 قابلیت دانلود عکس 
    &hashCode=[The hashCode]*



### بارگذاری فایل ها 

 کسب و کار می تواند فایل های خود را از هر نوع در پلتفرم  بارگذاری و هنگام نیاز دریافت نماید. جهت بارگذاری از سرویس زیر استفاده 
نمایید:

    HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
           POST
    Url: 
           [file-server-address]/nzh/uploadFile/
    Parametrs:
           fileName=[a name for the file]*
           file=[FILE: the file]*
            

توصیه می شود نام فایل شامل پسوند نوع فایل نیز باشد. برای مثال .pdf یا .mp3

در پاسخ درخواست بالا اطلاعات فایل آپلود شده به شرح زیر دریافت می گردد:

    {
        "hasError": false,
        "errorCode": 0,
        "count": 0,
        "ott": "65ef9560e28cb413",
        "result": {
            "id": 1430,
            "name": "test.xml",
            "hashCode": "163353f8242-0.6564397962118005"
        }
    }
برای دریافت فایل کافی است اطلاعات فایل را در سرویس زیر ارسال نمایید:

    GET [file-server-address]/nzh/file/
    ?fileId=[the id of uploaded file]*
    &downloadable=[true/false]	                                                          قابلیت دانلود فایل
    &hashCode=[The hashCode]*
            

**دسترسی سریع:**[پیوند](https://docs.pod.land/document/Developer-Introduction-Urls)

<div class="box-end">
</div>

## نقشه 
 در حوزه‌ی کسب‌وکار‌های مرتبط با گردشگری؛ استفاده از یک سرویس نقشه‌ی آنلاین کامل و دقیق، بسیار حائز اهمیت است.
با استفاده از سرویس نقشه می‌توانید برنامه‌ای را پیاده‌سازی کنید که به هر فرد، جاذبه‌های گردشگری نزدیک به او را نمایش دهد و اطلاعات مورد نیازش را برگرداند. برای مثال به او بگوید از نظر زمانی و مسافتی چقدر با آن مکان فاصله دارد، اطلاعات ترافیکی اطراف آن محل در آن لحظه چگونه است و … . علاوه بر این افراد می‌توانند با انتخاب شهر مورد نظرشان، مکان‌های تاریخی و گردشگری آن‌جا را روی نقشه مشاهده کنند و با انتخاب هر یک اطلاعات مربوط به آن برایشان نمایش داده شود. 

### جستجو
برای جستجوی نام خیابان‌ها، نام‌های قدیمی، اماکن و کسب و کارهای ثبت‌شده  بر روی نقشه (Location Based Search API) می‌توانید از وب‌سرویس جستجوی نشان استفاده کنید. این وب‌سرویس بهترین نتایج ممکن را با توجه به نقطه‌ی  مرجع (طول و عرض جغرافیایی مکانی که جستجو بایستی حول آن انجام شود) در  اختیار شما قرار می‌دهد. در پاسخ به هر درخواست جستجو حداکثر ۳۰ نتیجه‌ی  مرتبط توسط وب‌سرویس برگردانده می‌شود.
وب سرویس جستجوی مکان محور نقشه نشان یکی از کامل‌ترین سرویس‌های جستجو  مبتنی بر موقعیت ایرانی می‌باشد. این سرویس با پشتیبانی کامل از زبان فارسی و نگارش‌های مختلف از حروف فارسی، با توجه به موقعیت جغرافیایی مورد نظر  شما (نقطه مرجع) بهترین نتایج را به صورت مرتب‌شده بر اساس فاصله تا آن  نقطه مرجع در پاسخ باز می‌گرداند.
![توضیح تصویر](https://core.pod.land/nzh/image/?imageId=207561&width=800&height=200&hashCode=16c13231ecd-0.056176942445581135)

نقطه مرجع در این سرویس می‌تواند موقعیت جاری کاربر یا مرکز نقشه‌ای که کاربر مشاهده می‌کند باشد. این نقطه باید به‌صورت طول و عرض جغرافیایی( Latitude & Longitude) ارسال گردد. پارامتر نقطه‌ی مرجع به شما کمک می‌کند نتایج بهتری را در  خروجی داشته باشید. با توجه به معماری سرویس جستجوی مکان‌محور نشان، شما  محدودیتی در دریافت نتایج بسیار دور از نقطه‌ی مرجع (به عنوان مثال در شهری
 دیگر) را نیز نخواهید داشت. این نقطه می‌تواند مکان جغرافیایی کاربر نهایی  شما یا مرکز نقشه‌ای که مشاهده می‌کند باشد.

    HEADER:
        Api-Key=[YOUR_API_KEY]
    Method:
        GET
    Url:
        [base-url]/v1/search

شماره محصول برای فراخوانی به صورت سرویس کال: productId = **18913**
در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Api-Key نیست و شما بایستی پارامتر serviceCallToken را  مطابق توضیحاتی که در صفحه [نحوه استفاده از سرویس کال پاد](https://docs.pod.land/v1.0.8.0/Developer/ServiceCall/1231/ServiceCallUsage) آمده است تنظیم نمایید.

### پارامترهای ورودی

+ term: عبارت جستجو
+ lat: عرض جغرافیایی مرکز جستجو (latitude)
+ lng: طول جغرافیایی مرکز جستجو (longitude)
###  تبدیل موقعیت به آدرس 

از طریق وب‌سرویس تبدیل نقطه‌ی جغرافیایی به آدرس (Reverse Geocoding API ) به سادگی می‌توانید با ارسال طول و عرض جغرافیایی موردنظر، اطلاعاتی نظیر آدرس دقیق، نام محله، منطقه‌ی شهرداری، در طرح ترافیک بودن (تهران) و در  طرح زوج و فرد بودن (تهران، مشهد، اصفهان) آن نقطه را دریافت کنید.

	HEADER:
    Api-Key=[YOUR_API_KEY]
    Method:
    GET
    Url:
    [base-url]/v2/reverse
شماره محصول برای فراخوانی به صورت سرویس کال: productId = 15838

در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Api-Key نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحاتی که در صفحه [نحوه استفاده از سرویس کال پاد](https://docs.pod.land/v1.0.8.0/Developer/ServiceCall/1231/ServiceCallUsage) آمده است تنظیم نمایید.

####	پارامترهای ورودی

+ lat: عرض جغرافیایی مرکز جستجو (latitude)
+ lng: طول جغرافیایی مرکز جستجو (longitude)
### مسیریابی با درنظر گرفتن ترافیک 
پلتفرم نقشه نشان با بهره‌گیری از داده و مشارکت جامعه کاربران دو میلیونی  مسیریاب نشان، تنها ارائه‌دهنده ایرانی سرویس مسیریابی بر اساس دیتای  ترافیک آنلاین است.
با استفاده از وب‌سرویس مسیریابی (Direction API) شما می‌توانید بهترین  مسیر بین دو نقطه‌ی مشخص را به دست آورید. محاسبه مسیر با توجه به ترافیک  معابر محاسبه می‌شود و هر پاسخ ممکن است شامل یک یا چند مسیر باشد. در هر  مسیر زمان سفر و مسافت آن محاسبه می‌گردد. مرتب‌سازی مسیرها بر اساس بهترین مسیر از نظر زمان و مسافت خواهد بود.


    HEADER:
        Api-Key=[YOUR_API_KEY]
    Method:
        GET
    Url:
        [base-url]/v2/direction
    
    
شماره محصول برای فراخوانی به صورت سرویس کال: productId = 18916

در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Api-Key نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحاتی که در صفحه [نحوه استفاده از سرویس کال پاد](https://docs.pod.land/v1.0.8.0/Developer/ServiceCall/1231/ServiceCallUsage) آمده است تنظیم نمایید.

#### پارامترهای ورودی

+ و**origin:**مختصات نقطه شروع مسیریابی، این مختصات باید به صورت `latitude,longitude باشد که دو عدد با کاما از هم جدا شده‌اند.
+ و **destination:** مختصات نقطه پایان مسیریابی که قالب آن مانند نقطه شروع است.
+ و **waypoints:** این پارامتر اختیاری بوده و برای مشخص کردن نقاط میانی مسیر استفاده می‌شود. فرمت ارسال هر نقطه میانی به صورت`latitude,longitude` می‌باشد. در صورتی که بیش از یک نقطه میانی دارید با به صورت زیر آن‌ها را با علامت پایت (|) از هم جدا کنید: `latitude,longitude|latitude,longitude`
+ و **avoidTrafficZone:** این پارامتر اختیاری بوده و مقادیر آن `true` یا `false` می‌تواند باشد. در صورتی که این پارامتر true باشد مسیر از داخل طرح ترافیک عبور نخواهد کرد. همچین در صورتی که مقصد داخل طرح ترافیک باشد هیچ مسیری پیدا نمی‌شود.
+ و **avoidOddEvenZone:** این پارامتر اختیاری بوده و مقادیر آن `true` یا `false` می‌تواند باشد. در صورتی که این پارامتر true باشد مسیر از داخل طرح زوج و فرد عبور نخواهد کرد. همچین در صورتی که مقصد داخل طرح ترافیک باشد هیچ مسیری پیدا نمی‌شود.
+ و **alternative:** این پارامتر اختیاری بوده و مقادیر آن `true` یا `false` می‌تواند باشد. در صورتی که این پارامتر true باشد و مسیرهای جایگزین برای نقاط مشخص شده وجود داشته باشد این مسیرها در پاسخ ارائه خواهند شد. (مقدار پیش فرض این پارامتر false است)
با توجه به اینکه نام **طرح ترافیک** در شهرهای دیگر (غیر از تهران) عموماً یه جای **طرح زوج و فرد** نیز استفاده می‌شود، چنانچه در سایر شهرها هر یک از پارامترهای avoidTrafficZone و avoidOddEvenZone مقدار `true` داشته باشند و مقصد درون طرح زوج و فرد آن شهر باشد، سرویس مسیریابی خطای `NoRouteFound` در پاسخ برمی‌گرداند.
		
### مسیریابی بدون درنظر گرفتن ترافیک 
با استفاده از وب‌سرویس مسیریابی بدون در نظر گرفتن ترافیک (No Traffic Direction API) شما می‌توانید مسیرهای بین دو نقطه‌ی مشخص را به دست آورید. محاسبه مسیر با بدون در نظر گرفتن ترافیک معابر محاسبه می‌شودو هر پاسخ ممکن است شامل یک یا چند مسیر باشد. در هر مسیر زمان سفر و مسافت آن محاسبه می‌گردد. مرتب‌سازی مسیرها بر اساس بهترین مسیر از نظر زمان و  مسافت خواهد بود. 

    HEADER:
        Api-Key=[YOUR_API_KEY]
    Method:
        GET
    Url:
        [base-url]/v2/direction/no-traffic
            
            
   
   شماره محصول برای فراخوانی به صورت سرویس کال: productId = **18917**
   در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Api-Key نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحاتی که در صفحه [نحوه استفاده از سرویس کال پاد](https://docs.pod.land/v1.0.8.0/Developer/ServiceCall/1231/ServiceCallUsage) آمده است تنظیم نمایید.
   
####  پارامترهای ورودی
+ و**origin:**مختصات نقطه شروع مسیریابی، این مختصات باید به صورت `latitude,longitude` باشد که دو عدد با کاما از هم جدا شده‌اند.
+ و **destination:** مختصات نقطه پایان مسیریابی که قالب آن مانند نقطه شروع است.
+ و**waypoints:**این پارامتر اختیاری بوده و برای مشخص کردن نقاط میانی مسیر استفاده می‌شود. فرمت ارسال هر نقطه میانی به صورت `latitude,longitude` می‌باشد. در صورتی که بیش از یک نقطه میانی دارید با به صورت زیر آن‌ها را با علامت پایت (|) از هم جدا کنید:
`latitude,longitude|latitude,longitude`
+ و **avoidTrafficZone:**:این پارامتر اختیاری بوده و مقادیر آن `true` یا `false` می‌تواند باشد. در صورتی که این پارامتر true باشد مسیر از داخل طرح ترافیک عبور نخواهد کرد. همچین در صورتی که مقصد داخل طرح ترافیک باشد هیچ مسیری پیدا نمی‌شود.
+ و **avoidOddEvenZone:**: این پارامتر اختیاری بوده و مقادیر آن `true` یا `false` می‌تواند باشد. در صورتی که این پارامتر true باشد مسیر از داخل طرح زوج و فرد عبور نخواهد کرد. همچین در صورتی که مقصد داخل طرح ترافیک باشد هیچ مسیری پیدا نمی‌شود.
+ و **alternative:**: این پارامتر اختیاری بوده و مقادیر آن `true` یا `false` می‌تواند باشد. در صورتی که این پارامتر true باشد و مسیرهای جایگزین برای نقاط مشخص شده وجود داشته باشد این مسیرها در پاسخ ارائه خواهند شد. (مقدار پیش فرض این پارامتر false است)
با توجه به اینکه نام **طرح ترافیک** در شهرهای دیگر (غیر از تهران) عموماً یه جای **طرح زوج و فرد** نیز استفاده می‌شود، چنانچه در سایر شهرها هر یک از پارامترهای avoidTrafficZone و avoidOddEvenZone مقدار `true` داشته باشند و مقصد درون طرح زوج و فرد آن شهر باشد، سرویس مسیریابی خطای `NoRouteFound` در پاسخ برمی‌گرداند.

### ماتریس فاصله 
پلتفرم نقشه نشان با بهره‌گیری از داده و مشارکت جامعه کاربران دو میلیونی  مسیریاب نشان، تنها ارائه‌دهنده ایرانی سرویس ماتریس فاصله بر اساس دیتای ترافیک آنلاین است.
با استفاده از وب‌سرویس ماتریس فاصله (Distance Matrix API) میتوانید فاصله و زمان حرکت میان ماتریسی از نقاط شروع و پایانی را به دست آورید. تمامی  فواصل و زمان‌ها با در نظر گرفتن بهترین مسیر بر اساس وضعیت فعلی ترافیک  محاسبه می‌شوند.

    HEADER:
        Api-Key=[YOUR_API_KEY]
    Method:
        GET
    Url:
        [base-url]/v1/distance-matrix

شماره محصول برای فراخوانی به صورت سرویس کال: productId = **18911**

در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Api-Key نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحاتی که در صفحه [نحوه استفاده از سرویس کال پاد](https://docs.pod.land/v1.0.8.0/Developer/ServiceCall/1231/ServiceCallUsage) آمده است تنظیم نمایید.

#### پارامترهای ورودی
و  **origins:** لیستی از مختصات نقاط شروعی. هر کدام از این مختصات باید به فرم latitude,longitude باشند که با کاما (,) از یکدیگر جدا شده‌اند. در صورتی که تعداد مختصات  بیشتر از یک عدد باشد از علامت پایپ ( | ) برای جداسازی آنها استفاده  می‌شود.
و **destinations:** لیستی از مختصات نقاط پایانی که قالب آن مانند origins است.

### ماتریس فاصله بدون ترافیک 
پلتفرم نقشه نشان با بهره‌گیری از داده و مشارکت جامعه کاربران دو میلیونی  مسیریاب نشان، تنها ارائه‌دهنده ایرانی سرویس ماتریس فاصله بر اساس دیتای ترافیک آنلاین است.
 با استفاده از وب‌سرویس ماتریس فاصله (Distance Matrix API) میتوانید فاصله و زمان حرکت میان ماتریسی از نقاط شروع و پایانی را به دست آورید.در  محاسبات این سرویس وضعیت ترافیکی فعلی خیابان‌ها در نظر گرفته نمی‌شود. 

    HEADER:
        Api-Key=[YOUR_API_KEY]
    Method:
        GET
    Url:
        [base-url]/v1/distance-matrix/no-traffic

شماره محصول برای فراخوانی به صورت سرویس کال: productId = **18912**
در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Api-Key نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحاتی که در صفحه [نحوه استفاده از سرویس کال پاد](https://docs.pod.land/v1.0.8.0/Developer/ServiceCall/1231/ServiceCallUsage) آمده است تنظیم نمایید.

#### پارامترهای ورودی

+ و **origins:** لیستی از مختصات نقاط شروعی. هر کدام از این مختصات باید به فرم latitude,longitude باشند.
 که با کاما (,) از یکدیگر جدا شده‌اند. در صورتی که تعداد مختصات بیشتر از یک عدد باشد از علامت پایپ ( | ) برای جداسازی آنها استفاده می‌شود.
 
+ و **destinations:** لیستی از مختصات نقاط پایانی که قالب آن مانند origins است.

### نگاشت نقطه بر نقشه
سرویس نگاشت نقطه بر نقشه (Map Matching API) تعدادی نقاط ورودی را به  محتمل‌ترین مسیری که این نقاط نشان‌دهنده آن هستند، نگاشت میکند.

    HEADER:
        Api-Key=[YOUR_API_KEY]
    Method:
        GET
    Url:
        [base-url]/v1/map-matching

شماره محصول برای فراخوانی به صورت سرویس کال: productId = **18918**
در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Api-Key نیست و شما بایستی پارامترserviceCallToken  را مطابق توضیحاتی که در صفحه [نحوه استفاده از سرویس کال پاد](https://docs.pod.land/v1.0.8.0/Developer/ServiceCall/1231/ServiceCallUsage) آمده است تنظیم نمایید.
#### پارامترهای ورودی
+ و path: نقاطی که باید به یک مسیر نگاشت شوند. هر کدام از این نقاط با علامت پایپ ( | ) از یکدیگر جدا شده‌اند.مختصات هر نقطه به فرم latitude,longitude حداقل تعداد نقاط ورودی برابر با 2 است در غیر این صورت خطای 470 برگردانده می‌شود. 

<div class="box-end">
</div>


##  بن تخفیف

 در صورت نیاز به اعمال  تخفیف‌ بر روی محصولات مختلف مانند بلیط یا رزرو یا ... می‌توانید از این سرویس استفاده کنید. 

### بن شارژ اعتبار

جهت تعریف شارژ اعتبار، سرویس زیر را فراخوانی نمایید:

    Header:
    	_token_=[api_token]
    	_token_issuer_=1
    Method:  GET 
    URL:
            [platform-address]/nzh/biz/defineCreditVoucher
    Parameters:
            // برای ملاحظه پارامترها به لینک"تست و نمونه کد" مراجعه نمایید


توجه داشته باشید به ازای هر بن تخفیف، باید مقادیر تعداد، مبلغ، نام و توضیحات در پارامترهای جداگانه ارسال گردند.


### بن تخفیف مبلغی

برای ساخت بن تخفیف با مبلغ مشخص، سرویس زیر را فراخوانی نمایید؛ می‌توانید با یک بار فراخوانی سرویس، برای چند کاربر اعتبار تعریف نمایید، اما توجه داشته باشید به ازای هر کاربر، کد هش متفاوتی دریافت خواهید کرد و مشتری با اعمال کد هش می‌تواند از شارژ تعریف شده استفاده نماید.

جهت تعریف شارژ، لازم است در صنف خود حتما اعتبار داشته باشید، هم‌چنین می‌توانید کد هش را به صورت دلخواه تعریف نمایید.

    Header:
    	_token_=[api_token]
    	_token_issuer_=1
    Method:  GET 
    URL:
            [platform-address]/nzh/biz/defineDiscountAmountVoucher
    Parameters:
            // برای ملاحظه پارامترها به لینک"تست و نمونه کد" مراجعه نمایید


توجه داشته باشید به ازای هر بن تخفیف، باید مقادیر تعداد، مبلغ، نام و توضیحات در پارامترهای جداگانه ارسال گردند.


### بن تخفیف درصدی

جهت تعریف شارژ بن تخفیف، در قالب درصد سرویس ذیل را فراخوانی نمایید:

    Header:
    	_token_=[api_token]
    	_token_issuer_=1
    Method:  GET 
    URL:
            [platform-address]/nzh/biz/defineDiscountPercentageVoucher
    Parameters:
            // برای ملاحظه پارامترها به لینک"تست و نمونه کد" مراجعه نمایید


توجه داشته باشید به ازای هر بن تخفیف، باید مقادیر تعداد، درصد، نام و توضیحات در پارامترهای جداگانه ارسال گردند.

در صورت تعیین سقف مبلغ برای بن درصدی، در صورتی که بن بیش از یکبار قابل استفاده باشد، در دفعات بعدی مبلغ باقیمانده نسبت به سقف تعیین شده، قابل استفاده است.

در تعریف بن تخفیف درصدی **GuildCode** بعنوان حوزه ی مصرف بن اجباری است.

"guildCode":  نام صنف مطابق با صنف موجود در پنل می‌باشد.


### اعمال ووچر به فاکتور

بعد از تعریف ووچر، برای اعمال ووچر به فاکتور (درصورتی که پارامتر postVoucherEnabled در صدور فاکتور را با مقدار true ارسال نموده باشید)، سرویس ذیل را فراخوانی نمایید:

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

بن تخفیف جهت اعمال روی یک فاکتور، می‌تواند بیش از یک مورد باشد.


### دریافت و جستجو لیست بن‌ها

با سرویس زیر امکان خواهید داشت در بین لیست‌های بن کسب و کارتان جستجو و آن را دریافت نمایید:

    Header:
    	_token_=[api_token]
    	_token_issuer_=1
    Method:  GET 
    URL:
            [platform-address]/nzh/biz/getVoucherList
    Parameters:
            // برای ملاحظه پارامترها به لینک"تست و نمونه کد" مراجعه نمایید


توجه داشته باشید به ازای هر بن تخفیف، باید مقادیر تعداد، مبلغ، نام و توضیحات در پارامترهای جداگانه ارسال گردند.


### فعالسازی و غیرفعالسازی بن تخفیف

سرویس ذیل را جهت غیرفعال کردن بن تخفیف زودتر از موعد فراخوانی نمایید:

    Header:
    	_token_=[api_token]
    	_token_issuer_=1
    Method:  GET 
    URL:
            [platform-address]/nzh/biz/deactivateVoucher
    Parameters:
            id=


فعال نمودن مجدد بن تخفیف:

    Header:
    	_token_=[api_token]
    	_token_issuer_=1
    Method:  GET 
    URL:
            [platform-address]/nzh/biz/activateVoucher
    Parameters:
            id=

<div class="box-end">
</div>

## درگاه پرداخت
پرداخت از طریق درگاه اینترنتی یکی از آسان‌ترین و مهم‌ترین روش‌های پرداخت است. اگر می‌خواهید در برنامه خود از درگاه پرداخت اینترنتی استفاده کنید تا کاربران بتوانند به صورت اینترنتی و با استفاده از اطلاعات کارت بانکی خود هزینه‌های مربوطه را واریز کنند، می‌توانید از این سرویس استفاده کنید. این نکته را در نظر بگیرید که استفاده از درگاه پرداخت منوط به استفاده از کیف‌ پول پاد می‌باشد.

 .را از طریق سرویس زیر دریافت نمایید keyid برای انتقال کاربر به درگاه پرداخت اینترنتی، ابتدا باید مقدار
نحوه ارسال توکن: بعد از Bearer یک فاصله و سپس مقدار توکن ( _api_token_ موجود در پنل مدیریت کسب و کار) را قرار دهید.

نحوه ارسال شناسه مشتری: مقدار client_id (موجود در پنل مدیریت کسب و کار) را در انتهای url  قرار دهید. (بدون آکولاد)

```
HEADERS:
        Authorization=Bearer [_api_token_]
        Content-Type=application/x-www-form-urlencoded
Method: POST
Url:
        [sso-address]/oauth2/clients/handshake/{client_id}
Parameters:
        device_uid=[unique identity of device] *
```

<div class="box-end">
</div>

## کیف پول

روش‌های مختلفی برای پرداخت وجود دارد که یکی از آن‌ها از پرداخت از طریق کیف‌ پول است. 
با پیاده‌سازی سیستم کیف‌پول، در واقع شما در حساب کاربری افراد یک حساب بانکی مجازی ایجاد می‌کنید. هر یک از کاربران می‌توانند حساب مجازی خود را با هر مبلغی که بخواهند شارژ نمایند. پس از آن نیازی نیست کاربران برای پرداخت هزینه‌های خود اطلاعات کارت بانکی‌شان را وارد نمایند بلکه تنها با زدن دکمه‌ی پرداخت از طریق کیف پول، در کم‌ترین زمان ممکن و بسیار راحت هزینه‌های مربوطه را پرداخت خواهد کرد. توجه داشته باشید که استفاده از کیف پول پاد در کسب‌وکارهایی که می‌خواهند از سرویس‌های پاد استفاده کنند یکی از شروط اصلی است.
 
### شارژ کیف پول

مشتری ها برای شارژ کیف پول خود از طریق درگاه بانکی از لینک زیر استفاده می کنند. این لینک در سندباکس بدون نیاز به واریز پول واقعی کیف پول را شارژ می کند. کاربر از طریق این لینک به صفحه زیر هدایت می گردد:

- انتخاب بسته افزایشی
```
GET  [private-calls-address]/v1/pbc/BuyCredit/
?redirectUri=[redirectURL]
&callUri=[The function that will be called at the end of charge]
```



- انتقال مستقیم به درگاه با مبلغ معلوم

در این حالت کاربر صفحه انتخاب بسته را نمی بیند و مستقیماً وارد درگاه بانکی می گردد. برای این منظور کاربر را به صفحه زیر هدایت نمایید:

```
GET [private-calls-address]/v1/pbc/BuyCredit/
?amount= [the amount to charge wallet]
&redirectUri=[redirectURL]
&callUri=[The function that will be called at the end of charge]
```


پس از برگشت از درگاه مقادیر زیر به آدرس redirectUri برگردانده می شوند:

paid&tref

### افزایش موجودی مستقیم

در صورتی که مشتری شما در SSO پاد ثبت نشده است یا کیف پولی غیر از کیف پول پاد دارد، جهت افزایش موجودی او از طریق درگاه بانکی می توانید از سرویس زیر استفاده نمایید.

ابتدا توسط سرویس زیر یک فاکتور افزایش موجودی ایجاد نموده، سپس با hash ایجاد شده کاربر را به درگاه هدایت نمایید:

    HEADER:
            _token_=[api_token]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/issueCreditInvoiceAndGetHash
    Parameters:
            amount= *                        // مبلغ افزایش موجودی
            userId= *                     	//شناسه کاربر مربوط به مشتری
            billNumber= *	                // شماره قبض یکتا جهت جلوگیری از اجرای تراکنش تکراری
            wallet= *                            // کد کیف پول
            redirectUrl= *                      // آدرس برگشت پس از اتمام فرایند پرداخت با کارت بانکی

خروجی سرویس بالا شامل یک hash می باشد که فقط 15 دقیقه معتبر است:

```
{

  "hasError": false,

  "referenceNumber": "218789252",

  "errorCode": 0,

  "count": 0,

  "ott": "5cff51364b1c20a",

  "result": "d3bb4e8dbe2b4d3d94e0f056a7c61753"

}
```


مقدار آن را در آدرس زیر قرار داده و کاربر را به آن صفحه هدایت نمایید:

    MAIN server:
            https://core.pod.land/nzh/payAnyCreditInvoice?hash=&gateway=PEP
    
    SANDBOX server:
            https://sandbox.pod.land:8080/nzh/payAnyCreditInvoice?hash=&gateway=LOC

پس از شارژ توسط کاربر مقادیر زیر به آدرس برگشت برگردانده می شود:

tref=636980964366129546&payed=false&gws_rd=ssl

مقدار tref شماره پیگیری تراکنش شاپرکی می باشد و در این مرحله لازم است شارژ کیف پول توسط سرویس زیر تایید گردد:

```
HEADER:
        _token_=[api_token]
        _token_issuer_=1
Method: GET
Url:
        [platform-address]/nzh/biz/verifyCreditInvoice
Parameters:
       billNumber= * 	                // شماره قبض یکتا وارد شده در سرویس صدور فاکتور
```



در صورتی که عملیات پرداخت موفق نبوده باشد با تایید فاکتور شارژ کیف پول خطای 32 با پیغام "فاکتور قبلا لغو شده است" دریافت خواهید نمود.

### درخواست تسویه

کسب و کار می تواند با استفاده از API زیر درخواست انتقال وجه قابل تسویه موجود در حساب مجازی خود را بدهد. عملیات تسویه از طریق پنل نیز قابل انجام و پیگیری می باشد. همچنین میتوانید از طریق پنل کسب و کار خود یا وب سرویس برای یک حساب صنفی خاص یا کیف پول، تسویه اتوماتیک را فعال نمایید. به این ترتیب پایان هر شب مبلغ قابل تسویه موجود در آن حساب، به شماره شبای ثبت شده واریز می گردد.

**تسویه از طریق پنل کسب و کار**

#### تسویه از حساب مشتری (برداشت از کیف پول)

کسب و کار می تواند از طریق API زیر، مبلغ مورد نظر خود را از کیف پولش به شماره شبای ثبت شده در پروفایل خود منتقل کند. در صورتی که شماره شبا یا نام و نام خانوادگی شخص در پروفایل ثبت نشده باشد این سرویس خطا خواهد داد.

    HEADER:
            _token_=[API_TOKEN]            //توکن صاحب حساب
            _token_issuer_=1
            _ott_=[OTT]
    Method: GET
    Url: [platform-address]/nzh/requestSettlement/
    Parameters:
            amount=*                    //amount of money to cash out
            currencyCode=               //default:IRR
            uniqueId=                     //ارسال شناسه یکتا و دلخواه به منظور جستجو در لیست    // به منظور مشاهده تمام پارامترها به لینک تست و نمونه کد مراجعه نمایید

کد ارز شامل کد سه حرفی رایج برای واحدهای پولی است. مانند IRR و USD

#### تسویه از حساب صنفی کسب و کار

در حساب های صنفی همواره مبلغی به عنوان مبلغ قابل تسویه وجود دارد که شامل دارایی کسب و کار بجز فاکتورهای باز او یا فاکتورهایی که مبلغ آن ها هنوز واریز نشده است، می باشد. مبلغ قابل تسویه را می توان از طریق API زیر تسویه نمود:

    HEADER:
            _token_=[API_TOKEN]
            _token_issuer_=1
            _ott_=[OTT]
    Method: GET
    Url: [platform-address]/nzh/biz/requestSettlement/
    Parameters:
            amount=[value]*
            guildCode=[GUILD_CODE]*
            firstName=[first name of account holder]
            lastName=[last name og account holder]
            sheba=[sheba number without IR]		//اگر داده نشود همان مقدار ثبت شده در کسب و کار استفاده میشود
            currencyCode=[CURRENCY_CODE]
            uniqueId=                                           //ارسال شناسه یکتا و دلخواه به منظور جستجو در لیست

`
**انتقال وجه از حساب کسب و کاری به کارت بانکی (با کسر کارمزد) یا شماره شبا**

کسب و کار می تواند با استفاده از سرویس زیر مبلغ مورد نظر خود را از حساب مجازی به یک شماره کارت یا یک شماره شبا بانکی منتقل نماید. بدیهی است که در صورت استفاده از ابزار کارت به کار، کارمزد بانکی از حساب کسب و کار کسر خواهد شد و در صورت استفاده از ابزار پایا، انتقال وجه در زمان مصوب بانک مرکزی انجام خواهد شد.

برای پارامتر toolCode از یکی از مقادیر زیر استفاده نمایید:

SETTLEMENT_TOOL_SATNA

SETTLEMENT_TOOL_PAYA

SETTLEMENT_TOOL_CARD

و به طور مثال، در صورتی که انتقال از طریق کارت را انتخاب نموده اید، در قسمت toolId شماره کارت مقصد را وارد نمایید و در غیر این صورت شماره شبا را وارد نمایید.

 

    HEADER:
            _token_=[API_TOKEN]
            _token_issuer_=1
            _ott_=[OTT]
    Method: GET
    Url:
            [platform-address]/nzh/biz/requestSettlementByTool
    Parameters:
            firstName=
            lastName=
            toolCode= [one of the above tools]*
            toolId= [value of mentioned tool]*
            guildCode= [GUILD CODE]*
            amount= [AMOUNT]*
            uniqueId=                     //ارسال شناسه یکتا و دلخواه به منظور جستجو در لیست

``
**گزارش وضعیت تسویه**

جهت دریافت لیست تسویه ها و وضعیت آن ها از سرویس زیر استفاده نمایید:

  

    HEADER:
            _token_=[API_TOKEN]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/listSettlements/
    Parameters:
            size=[pagination size]*
            offset=[pagination offset]*
            statusCode= [status of settlement from below table]
            fromAmuont= [lower limit of requested amount]
            toAmount= [upper limit of requested amount]
        


| ستون 1               | ستون 2                                  |
| -------------------- | --------------------------------------- |
| **statusCode**       | **شرح**                                 |
| SETTLEMENT_DONE      | تسویه حساب انجام شده است                |
| SETTLEMENT_REQUESTED | تسویه درخواست داده شده و تایید نشده است |
| SETTLEMENT_SENT      | تسویه تایید شده و ارسال شده است         |


**فعالسازی تسویه خودکار**

در صورتی که تسویه خودکار برای یک کسب و کار فعال شود، مبلغ قابل تسویه آن کسب و کار به طور خودکار، یکبار در شبانه روز به شماره شبای اعلام شده در پروفایل کسب و کار یا شماره شبای اعلامی در سرویس زیر، تسویه می گردد. برای فعالسازی تسویه خودکار سرویس زیر را با توکن کسب و کار دارنده حساب فراخوانی نمایید:

    HEADER:
            _token_=API_TOKEN           //توکن دارنده حساب
            _token_issuer_=1
            _ott_=OTT                     //توکن یکبار مصرف
    Method: GET
    Url: [platform-address]/nzh/biz/addAutoSettlement/
    Parameters:
            guildCode=*                   //GUILD_CODE
            firstName=                     //first name of account holder
            lastName=                     //last name og account holder
            sheba=                        //sheba number without IR 
            currencyCode=               //default=IRR

**لغو تسویه خودکار**

با سرویس ذیل می‌توانید تسویه خودکار را غیرفعال نمایید:

    HEADER:
            _token_=API_TOKEN           //توکن دارنده حساب
            _token_issuer_=1
    Method: GET
    Url: [platform-address]/nzh/biz/removeAutoSettlement/
    Parameters:
            guildCode=*                   //GUILD_CODE
            currencyCode=                //default=IRR

### انتقال وجه کاربر به کاربر

**انتقال وجه میان حساب مجازی کسب و کار و کیف پول همان کاربر**

کسب و کار باید سرویس زیر را برای این منظور صدا بزند. دقت نمایید که مبالغی که منتقل می شوند باید تراز باشند، یعنی جمع مقادیر صفر شود. در شبه کد زیر، اعتبار از حساب صنفی به حساب کیف پول کسب و کار منتقل می گردد.

    HEADER:
            _token_=[API_TOKEN]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/transferFromOwnAccounts
    Parameters:
            guildCode=[GUILD CODE]	        //میتواند لیستی از صنف ها باشد
            amount= -[AMOUNT]		//میتواند لیستی از مقادیر باشد که طولش با طول لیست صنفها برابر است
            customerAmount= +[AMOUNT]
            uniqueId=                            //ارسال شناسه دلخواه و یکتا به منظور جستجو در لیست 

لیست انتقال‌های بین حساب‌های مجازی و کیف پول خود را با سرویس زیر دریافت نمایید:

هم‌چنین می‌توانید با لحاظ شناسه یکتا برای انتقال‌های خود(uniqueId) نسبت به جستجو بر اساس همان شناسه اقدام نمایید.

    HEADER:
            _token_=[API_TOKEN]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/transferFromOwnAccountsList
    Parameters:
            uniqueId= // امکان جستجو بر اساس شناسه یکتای ارسالی در انتقال
            offset=*
            size=*
            fromDate=
            toDate=

**انتقال وجه از کیف پول به کیف پول کاربر دیگر (مخاطب)**

کاربر می تواند مبلغی از اعتبار موجود در کیف پول خود را به کاربر دیگر که لازم است جزء مخاطبین او باشد، انتقال دهد. ثبت مخاطبان کاربر از طریق شماره موبایل یا ایمیل یا نام کاربری یا همه آنها صورت می گیرد. سپس از طریق سرویس زیر امکان انتقال وجه به مخاطب برای کاربر فراهم می گردد:

    HEADER:
            _token_=[access_token]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/transferToContact
    Parameters:
            contactId = *            //شناسه مخاطب مقصد برای انتقال اعتبار
            amount = *
            wallet =PODLAND_WALLET           //کد کیف پول
            currencyCode =
            description =             // توضیحات
            uniqueId=                //ارسال شناسه دلخواه و یکتا به منظور جستجو در لیست

و با سرویس زیر لیست انتقال‌ها را دریافت کنید:

هم‌چنین می‌توانید با لحاظ شناسه یکتا برای انتقال‌های خود(uniqueId) نسبت به جستجو بر اساس همان شناسه اقدام نمایید.

    Header:
            _token_ = [access_token]
            _token_issuer_ = 1    
    Method: GET
    url: [platform-address]/nzh/transferToContactList
    Parameters:
            contactId = *          //شناسه مخاطب مقصد برای انتقال اعتبار
            currencyCode =
            uniqueId =            //ارسال شناسه دلخواه و یکتا به منظور جستجو در لیست
            size = *
            offset = *
            fromAmount =
            toAmount =
            fromDate = 
            toDate =
            uniqueId= //امکان جستجو بر اساس شناسه یکتا

### ‌‌دنبال کردن کسب وکار

برای انجام عملیات کیف پول، مانند سایر سرویس های پلتفرم، باید کاربر جزو دنبال کنندگان کسب و کار شما باشد تا بتوانید از برخی سرویس های پلتفرم(از جمله، انتقال اعتبار به مشتریان) استفاده نمایید.

ضمنا اگر خودتان اقدام به ثبتنام کاربران نموده اید، به طور اتومات آن ها جزء مشتریان شما خواهند شد.(برای آزمون درستی این بخش، سرویس nzh/biz/getFollowers را فراخوانی نمایید.)

توجه داشته باشید کاربر باید در پاد لاگین باشد و با داشتن توکن جاری کاربر و فراخوانی آن در سرویس زیر، می‌توانید کاربر را به دنبال کنندگان کسب و کار خود(لیست مشتریان)، اضافه نمایید:

    HEADER  _token_=[access_token] & _token_issuer_=1
    POST [platform-address]/nzh/follow/
    ?businessId=[businessid]		کد شناسایی کسب و کار
    &follow=true 

در این سرویس نیز شناسایی کاربر از روی توکن دریافت شده در هدر انجام می شود و در صورت موفقیت پاسخ زیر را برمی گرداند:

    {
    	"hasError": false,
    	"errorCode": 0,
    	"count": 0,
    	"ott": "d0884d219728c624",
    	"result": true
    }

توجه داشته باشید که businessId کد شناسایی کسب و کار شما می باشد. در صورتی که آن را ندارید از سرویس زیر برای دریافت آن استفاده کنید:

    GET [platform-address]/nzh/biz/getBusiness/?_token_=[API_TOKEN]&_token_issuer_=1

برای دریافت لیست دنبال کنندگان کسب و کار خود از سرویس زیر استفاده نمایید:

    HEADER:
            _token_=[API_TOKEN]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/getFollowers/
    Parameters:
            size= [pagination size]*
            offset= [pagination offset]*

### انتقال وجه به مشتریان

مشتریان یا دنبال کنندگان کسب و کار از گروه های زیر تشکیل می شوند:

+ همان مشتریان او هستند که پس از صدور فاکتور (چه پرداخت شود یا نشود) دنبال کننده می شوند.
+ کسب و کارهایی که توسط یک کسب و کار دیگر ایجاد می شوند.
+ کاربرانی که از درگاه های معرفی کسب و کارها خودشان کسب و کار را دنبال می کنند.
+ کابرانی که اطلاعات آنها  توسط کسب و کار ثبت می شود

کسب و کار می تواند از طریق API زیر، مبلغ مورد نظر خود را به کیف پول دنبال کنندگان خود انتقال دهد:

    HEADER:
            _token_=[api_token]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/transferToFollower/
    Parameters:
            userId=[userId]*		          شناسه کاربر دنبال کننده
            guildCode= [ کد صنف ] *
            amount= [ مبلغ انتقال ] *
            description=                        شرح انتقال
            currencyCode= [IRR/USD/...]     کد ارز
            wallet=PODLAND_WALLET   
            uniqueId=    // ارسال شناسه دلخواه و یکتا به منظور امکان جستجو در لیست ها بر اساس شناسه یکتا 

سرویس زیر نیز برای انتقال وجه به مشتریان به کار می رود با این تفاوت که پس از فراخوانی این سرویس مشتری یک پیامک شامل موارد زیر دریافت می کند و در صورتی که کد لغو را ارسال ننماید مبلغ به شماره شبا موجود در پروفایل کاربر منتقل می گردد. در صورت ارسال کد لغو در پیامک، مبلغ منتقل شده، در کیف پول کاربر تا مراجعه یا خرید بعدی باقی می ماند.
+ مبلغ دریافتی
+ اطلاعات شماره شبا
+ نام و نام خانوادگی صاحب حساب
+ کد امنیتی


    HEADER:
            _token_=[api_token]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/transferToFollowerAndCashout
    Parameters:
            userId=[userId]*		         شناسه کاربر
            guildCode= [ کد صنف ] *
            amount= [ مبلغ انتقال ] *
            description= *                       شرح انتقال
            currencyCode= [IRR/USD/...]     کد ارز
            wallet=PODLAND_WALLET    
            uniqueId=    // ارسال شناسه دلخواه و یکتا به منظور امکان جستجو در لیست ها بر اساس شناسه یکتا 

**دریافت لیست انتقال‌ها به مشتریان و امکان جستجو بر اساس شناسه یکتا:**

با سرویس زیر، لیست انتقال‌ها را دریافت نمایید:

    HEADER:
            _token_=[api_token]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/transferToFollowerList
    Parameters:
            userId=
            guildCode=
            wallet=
            currencyCode=IRR
            fromAmount=// تاریخ شمسی
            toAmount=// تاریخ شمسی
            uniqueId=
            offset=*
            size=*
            fromDate=
            toDate=
           

**انتقال به مشتریان بر اساس فاکتور:**

این سرویس در شرایطی فراخوانی می‌گردد که نیاز است مبلغی با توجه به فاکتور صادر شده، از کسب و کار به مشتری منتقل گردد. اگر فاکتور ارسالی، هنوز بسته نشده باشد نمی‌توانید این سرویس را فراخوانی نمایید و برای تغییر مبلغ فاکتور، لازم است فاکتور را کنسل نموده  و مجددا به مبلغ دلخواه فاکتور را صادر نمایید.

اگر فاکتور متعلق به صاحب توکن نباشد، "پیغام مجوز ندارید" دریافت خواهید کرد.

این انتقال مبلغ می‌تواند از حساب مشتری(کیف پول پاد) و یا از صنف کسب و کار در صورتی که مبلغ قابل تسویه داشته باشد، انجام گیرد. اگر direct debit فعال باشد، به طور اتومات از حساب اصلی کسر خواهد شد.

نحوه انتقال پول، بر اساس نحوه پرداخت فاکتور ارسالی، خواهد بود. به عنوان مثال، اگر پرداخت فاکتور به صورت نقدی بوده است، انتقال به مشتری با فراخوانی این سرویس ممکن نخواهد بود و در ریسپانس دریافتی از فراخوانی سرویس، همان مبلغ موجود در حساب کسب و کار(کیف پول و صنفی) برگردانده خواهد شد.


    HEADER:
            _token_=[api_token]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/transferByInvoice
    Parameters:
            guildCode= // ارسال یکی از پارامترهای کد صنف و کیف پول اجباری می‌باشد 
            amount= [ مبلغ انتقال، ریال ] *
            description= *   //          شرح انتقال
            currencyCode= [IRR]     کد ارز
            wallet=PODLAND_WALLET     // ارسال یکی از پارامترهای کد صنف و کیف پول اجباری می‌باشد 
            invoiceId= *
            uniqueId=   // ارسال شناسه دلخواه و یکتا به منظور امکان جستجو در لیست ها بر اساس شناسه یکتا 

**لیست انتقال به مشتریان بر اساس فاکتور:**

با سرویس زیر می‌توانید لیست انتقالات بر اساس فاکتور را دریافت نمایید.

    HEADER:
            _token_=[api_token]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/biz/listTransferByInvoice
    Parameters:
            invoiceId=
            guildCode=
            wallet=
            currencyCode=IRR
            fromAmount=
            toAmount=
            uniqueId= // امکان جستجو بر اساس شناسه یکتا در لیست انتقالات
            offset= *
            size= *
            fromDate=// تاریخ شمسی
            toDate=// تاریخ شمسی

### دریافت صورتحساب

توسط سرویس زیر می ­توانید تمام تراکنش­ هایی که در حساب­ های صنفی کسب و کار شما انجام شده را دریافت و مشاهده نمایید:


    HEADER:
            _token_=<API_TOKEN> 		توکن کسب و کار
            _token_issuer_=1
    METHOD: POST
    Url:  [platform-address]/nzh/biz/getAccountBill
    Parameters:
    	size=*				اندازه لیست خروجی
    	offset=*				فاصله از مبدا لیست خروجی
    	dateFrom=			حد پایین تاریخ صورتحساب
    	dateTo=				حد بالای تاریخ صورتحساب
    	description=			جستجوی در شرح صورتحساب
    	amountFrom=			حد پایین مبلغ صورتحساب
    	amountTo=			حد بالای مبلغ صورتحساب
    	guildCode=			کد صنف مبداء کسب و کار

همچنین از طریق سرویس زیر صورتحساب روی کیف پول خود را دریافت می نمایید:

    HEADER:
            _token_=<API_TOKEN> 		توکن کسب و کار
            _token_issuer_=1
    METHOD: POST
    Url:  [platform-address]/nzh/getAccountBill
    Parameters:
    	size=*				اندازه لیست خروجی
    	offset=*				فاصله از مبدا لیست خروجی
    	dateFrom=			حد پایین تاریخ صورتحساب
    	dateTo=				حد بالای تاریخ صورتحساب
    	description=			جستجوی در شرح صورتحساب
    	amountFrom=			حد پایین مبلغ صورتحساب
    	amountTo=			حد بالای مبلغ صورتحساب
    	wallet=PODLAND_WALLET	کد کیف پول

هم چنین امکان دریافت صورتحساب در قالب یک فایل اکسل وجود دارد.

ارسال یکی از پارامترهای dateFrom یا dateTo اجباری است. در صورت ارسال پارامتر dateFrom ارسال dateTo اختیاری است و بالعکس.

    HEADER:
            _token_=<API_TOKEN> 		توکن کسب و کار
            _token_issuer_=1
    METHOD: GET
    Url:  [platform-address]/nzh/biz/getAccountBillAsFile
    Parameters:
            dateFrom= 
            dateTo=

### گزارش انتقال وجوه به کارت

در لیست کارت به کارت ها می‌توانید تراکنش هایی که به یکی از سه طریق زیر صورت گرفته است را دریافت نمایید:

1- خرید از طریق درگاه بانکی و پرداخت با کارت و برگشت فاکتور:

در این حالت قبل از بستن فاکتور، لغو فاکتور انجام شده است پس causeCode برابر با CASHOUT_CAUSE_TYPE_INVOICE خواهد بود.

همانطور که در بخش  بستن فاکتور توضیح داده شد، امکان لغو فاکتوری که بسته شده است وجود ندارد، لذا در صورتی که تمایل به کنسل نمودن فاکتور دارید، باید سرویس transferByInvoice را فراخوانی نمایید.

2- خرید از طریق درگاه بانکی و پرداخت با کارت و انتقال اعتبار به کارت مشتری بر اساس فاکتور بسته شده:

در این حالت، causeCode تراکنش برابر با CASHOUT_CAUSE_TYPE_SETTLEMENT خواهد بود.

3- درخواست تسویه با کارت:

در صورت ثبت درخواست برای تسویه از کیف پول مجازی به شماره کارت، causeCode برابر با CASHOUT_CAUSE_TYPE_SETTLEMENT خواهد بود.

مقدار statusCode که در پاسخ فراخوانی سرویس زیر برگردانده می‌شود، وضعیت کارت به کارت را اعلام مینماید، این وضعیت یکی از چهار حالت ذیل می‌باشد:

1-  CARD_TO_CARD_STATUS_SENDING

2- CARD_TO_CARD_STATUS_SUCCESSFUL

3- CARD_TO_CARD_STATUS_FAILED

4- CARD_TO_CARD_STATUS_CREATED


    Header:
        _token_=[API_TOKEN]
        _token_issuer_=1
    Method: GET
    Url: [platform-address]/nzh/biz/cardToCardList/
    Parameters:
        size=[the required count of result list]*
        offset=[the offset of beginning of result list]*
        canEdit=
        canceled=
        statusCode=
        causeCode=
        causeId=
        fromDate=
        toDate
        fromAmount=
        toAmount=
        referenceNumber=
        uniqueId=                   //the uniqueId used in card transfer order

خروجی سرویس در صورتی که hasError=false باشد در بخش result  به شکل زیر است:

```
[
  {
    "id": 0,
    "statusCode": "string",
    "creationDate": "epoch 13 digits timestamp",
    "doneDate": "epoch 13 digits timestamp",
    "canEdit": true,
    "causeId": "string",
    "causeCode": "string",
    "referenceNumber": "string",
    "uniqueId": "string",
    "items": [
      {
        "id": 0,
        "amount": 0,
        "description": "string",
        "destCardNumber": "string",
        "trackingId": "string",
        "doneDate": "epoch 13 digits timestamp",
        "cardToCardPoolLogList": [
          {
            "message": "string",
            "success": true,
            "date": "epoch 13 digits timestamp"
          }
        ]
      }
    ]
  }
]
```


مقدار causeId برابر با شناسه settlementای است که باعث انجام کارت به کارت شده است.

به عنوان مثال در سرویس درخواست تسویه به کارت، causeId برابر با شناسه درخواست تسویه می‌باشد.

ممکن است اطلاعات کارت مقصد اشتباه باشد یا قابلیت واریز به آن وجود نداشته باشد، در این صورت تراکنش به وضعیت CARD_TO_CARD_STATUS_FAILED می رود. 

اگر در لیست کارت به کارت های خود، کارت به کارتی با وضعیت CARD_TO_CARD_STATUS_FAILED و با مقدار true برای canEdit داشته باشید، می‌توانید آن را با سرویس آپدیت کارت به کارت، مجددا فراخوانی نمایید؛ این وضعیت برای کارت به کارت هایی ایجاد می شود که با ابطال خرید (cancelInvoice) یا کاهش فاکتور (reduceInvoice) ایجاد شده اند و خریدار با کارت بانکی غیر قابل واریز خرید را انجام داده باشد. به عنوان مثال، ممکن است خرید با کارت هدیه صورت گرفته باشد و مبلغ قابل واریز به کارت هدیه نباشد، در این صورت بعد از گذشت حداکثر 15 دقیقه، مقدار canEdit در پاسخ true برگردانده می‌شود و می‌توانید شماره کارت را ویرایش نمایید.

همچنین در برخی موارد که کارت به کارت دچار وضعیت CARD_TO_CARD_STATUS_FAILED می گردد، مبلغ کارت به کارت به صورت کامل به حساب مبدا برگردانده می شود. این موارد شامل کارت به کارت هایی است که با دستور تسویه به کارت (requestSettlementByTool) یا انتقال وجه بر اساس فاکتور (transferByInvoice) ایجاد شده باشد.

توجه داشته باشید شناسه کارت به کارت، در آبجکت items برگردانده می‌شود.

    Header:
           _token_=[API_TOKEN]
           _token_issuer_=1
    Method: GET
    Url: [platform-address]/nzh/biz/updateCardToCard
    Parameters:
            id= // شناسه کارت به کارت
            cardNumber= // شماره کارت

<div class="box-end">
</div>

## فاکتور
با استفاده از این سرویس، شما می‌توانید برای هر پرداختی که کاربران انجام می‌دهند، فاکتور صادر کنید. این فاکتور شامل اطلاعات کاملی از قبیل نام و نام خانوادگی فرد واریز کننده مبلغ، علت پرداخت وجه، تاریخ پرداخت وجه و ... می‌باشد. همچنین در صورت لزوم می‌توانید از زیرسرویس‌هایی مانند استرداد یا کاهش فاکتور نیز استفاده نمایید و بدون نیاز به گرفتن اطلاعات حساب از مشتری، به صورت خودکار، کل مبلغ و یا قسمتی از آن را به حساب او برگردانید.

### صدور فاکتور توسط کسب وکار 
هرگونه پرداخت در پلتفرم پاد، از طریق فاکتور صورت می گیرد. در این بخش صدور فاکتور با استفاده از توکن کسب و کار شرح داده شده و می توان با خروجی حاصل از این متد، کاربر را به راحتی به درگاه پرداخت هدایت نمود. برای  صدور فاکتور از سرویس زیر استفاده نمایید. شبه کد زیر یک فاکتور با دو بند  فاکتور را شامل می شود:
پارامترهای اختیاری کامنت شده اند,برای استفاده می توانید از حالت کامنت خارج کنید.


```
var output = new ResultSrv<InvoiceSrv>();
                var invoiceSrv = IssueInvoiceVo.ConcreteBuilder
                    .SetGuildCode("{put your guildCode}")
                    .SetProductsInfo(new List<ProductInfo>
                    {                         
               ProductInfo.ConcreteBuilder.SetProductId(0).SetPrice(1000).SetQuantity(3).SetProductDescription("tst1").Build(),                         
                ProductInfo.ConcreteBuilder.SetProductId(0).SetPrice(1000).SetQuantity(3).SetProductDescription("tst1").Build()
                    })
                    .SetOtt("{Put your ott}")
                    //.SetPreview({put your preview})
                    //.SetMetadata("{put your metadata}")
                    //.SetUserId({put user id})
                    //.SetAddressId("{put your addressId}")
                    .Build(); // Create new instance 
 billingService.IssueInvoice(invoiceSrv, response => Listener.GetResult(response, out output));

```


### لیست آدرس

در صورتی که تمایل به ارسال آدرس مشتری دارید، از طریق سرویس زیر شناسه‌های آدرس‌های موجود برای کاربر را استخراج نمایید.
 پارامترهای اختیاری کامنت شده اند,برای استفاده می توانید از حالت کامنت خارج کنید.

```
 var output = new ResultSrv<AddressSrv>();
                var invoiceSrv = ListAddressVo.ConcreteBuilder
                    .SetOffset("0")
                    //.SetSize("")
                    .Build();
 billingService.GetListAddress(invoiceSrv, response => Listener.GetResult(response, out output));

```


### تایید پرداخت فاکتور

در صورتی که در صدور فاکتور پارامتر verificationNeeded را با مقدار true  ارسال نموده باشید، پرداخت سه مرحله ای فعال شده است. به این معنی که پس از هدایت کاربر به صفحه پرداخت(فقط در صورت پرداخت فاکتور از طریق اتصال به  درگاه می توانید سرویس تایید فاکتور را صدا بزنید) و دریافت پاسخ در redirectUri لازم است پرداخت توسط کسب و کار با استفاده از API زیر تایید شود. 
در صورتی که فاکتور مورد نظر تسهیمی است، شناسه ای که باید به این سرویس  ارسال گردد، معادل result -> id موجود در خروجی فاکتور تسهیمی می باشد.
پارامترهای اختیاری کامنت شده اند,برای استفاده می توانید از حالت کامنت خارج کنید.

```
var output = new ResultSrv<InvoiceSrv>();
var verifyInvoiceVo = VerifyInvoiceVo.ConcreteBuilder
                    .SetId({put your id})
                    //.SetBillNumber("{put your billNumber}")
                    .Build();
billingService.VerifyInvoice(verifyInvoiceVo, response => Listener.GetResult(response, out output));
```


### بستن فاکتور
فاکتور هایی که بسته شوند دیگر قابل ابطال نیستند. برای اینکه بتوانید مبالغ فروش خود را تسویه نمایید لازم است حتما فاکتورها را ببندید.

```
var output = new ResultSrv<bool>();
var closeInvoiceVo = CloseInvoiceVo.ConcreteBuilder
                    .SetId({put your id})
                    .Build();
billingService.CloseInvoice(closeInvoiceVo, response => Listener.GetResult(response, out output));

```


### تایید و بستن در یک مرحله
با فراخوانی سرویس زیر، می‌توانید همزمان تایید و بستن فاکتور را انجام دهید.

```
var output = new ResultSrv<InvoiceSrv>();
var verifyAndCloseInvoiceVo = VerifyAndCloseInvoiceVo.ConcreteBuilder
                    .SetId({put your id})
                    .Build();
billingService.VerifyAndCloseInvoice(verifyAndCloseInvoiceVo,response => Listener.GetResult(response, out output));

```

### ابطال فاکتور
در صورتی که فاکتور باطل شود، دیگر قابل پرداخت نیست و در صورتی که قبلا پرداخت شده باشد، مبلغ آن به پرداخت کننده برگشت خواهد خورد. 
توجه: در صورتی که فاکتور با شرایط safe=true صادر شده باشد، فقط پرداخت  کننده می تواند فاکتور را کنسل کند و اگر safe نباشد فقط issuer فاکتور  مجاز به کنسلی فاکتور می باشد. 
```
var output = new ResultSrv<bool>();
var cancelInvoiceVo = CancelInvoiceVo.ConcreteBuilder
                    .SetId({put your id})
                    .Build();
billingService.CancelInvoice(cancelInvoiceVo, response => Listener.GetResult(response, out output));
```


### دریافت فاکتور
با فراخوانی سرویس زیر می توانید فاکتورهایی که کسب و کار شما صادر نموده و همچنین وضعیت آنها را مشاهده نمایید.

```
var output = new ResultSrv<List<InvoiceSrv>>();
var getInvoiceListVo = GetInvoiceListVo.ConcreteBuilder
                    .SetSize({Put your size})
                    .SetOffset({Put your offset})
                    //.SetGuildCode("{put your guildCode}")
                    .Build();
billingService.GetInvoiceList(getInvoiceListVo, response => Listener.GetResult(response, out output));

```

### دریافت فاکتور با متا دیتا
از طریق این سرویس می توانید تمام فاکتورهایی که برای آنها متادیتا تعریف کرده اید دریافت کنید. 
در قسمت metaQuery مقادیر درخواستی خود را به فرم json با استفاده از توصیحات جستجوی متادیتا ارسال نمایید.
https://docs.pod.land/v1.0.8.0/Developer/CustomPost/400/SearchMetadata

```
var output = new ResultSrv<List<InvoiceSrv>>();
var getInvoiceListByMetadataVo = GetInvoiceListByMetadataVo.ConcreteBuilder
                    //.SetMetaQuery("{Put your metaQuery}")
                    //.SetSize({Put your size})
                    //.SetOffset({Put your offset})
                    //.SetIsCanceled({put your value})
                    //.SetIsPayed({put your value})
                    .Build();
billingService.GetInvoiceListByMetadata(getInvoiceListByMetadataVo, response => Listener.GetResult(response, out output));
```

### دریافت لیست فاکتورها در قالب فایل
از طریق سرویس زیر امکان دریافت لیست فاکتورها در قالب فایل وجود دارد. 
وارد کردن یکی از فیلدهای زیر ضروری است : lastNRows,fromDate,toDate

```
var output = new ResultSrv<InvoiceSrv>();
var getInvoiceListAsFileVo = GetInvoiceListAsFileVo.ConcreteBuilder
                    .SetLastNRows({Put your LastNRows})
                    //.SetFromDate({Put your FromDate})
                    //.SetToDate({Put your ToDate})
                    //.SetGuildCode("{Put your GuildCode}")
                    //.SetId({Put your Id})
                    //.SetBillNumber("{Put your BillNumber}")
                    //.SetUniqueNumber("{Put your UniqueNumber}")
                    //.SetTrackerId({Put your TrackerId})
                    //.SetIsCanceled({Put your IsCanceled})
                    //.SetIsClosed({Put your IsClosed})
                    //.SetIsPayed({Put your IsPayed})
                    //.SetIsWaiting({Put your IsWaiting})
                    //.SetReferenceNumber("{Put your ReferenceNumber}")
                    //.SetUserId({Put your UserId})
                    //.SetQuery("{Put your Query}")
                    //.SetProductIdList({Put your ProductIdList})
                    //.SetCallbackUrl("{Put your CallbackUrl}")
                    .Build();
billingService.GetInvoiceListAsFile(getInvoiceListAsFileVo,response => Listener.GetResult(response, out output));

```


### کاهش فاکتور
در مواردی ممکن است نیاز به تغییری در بندهای فاکتور داشته باشید. در صورتی که فاکتور پرداخت نشده است، فاکتور قبلی را باطل (cancel) نمایید و فاکتور جدیدی صادر کنید. اگر فاکتور پرداخت شده است(در صورتی که باید پول بیشتری از مشتری دریافت نمایید)، لازم است فاکتوری جداگانه به مبلغ افزوده شده، با ذکر دلیل صادر نموده و مشتری را مجددا برای پرداخت هدایت نمایید. در برخی مواقع لازم است مبلغی از فاکتور پرداخت شده به مشتری بازگردانده شود. برای این منظور از API زیر برای اصلاح فاکتور پرداخت شده استفاده نمایید.

```
var output = new ResultSrv<InvoiceSrv>();
var reduceInvoiceVo = ReduceInvoiceVo.ConcreteBuilder
                    .SetId({Put your id})
                    .SetInvoiceItemsInfo(new List<InvoiceItemInfoVo>
                    {
                        InvoiceItemInfoVo.ConcreteBuilder.SetInvoiceItemId({Put your id}).SetItemDescription("{Put your description}").SetPrice({Put your price}).SetQuantity({Put your quantity}).Build(),
                        InvoiceItemInfoVo.ConcreteBuilder.SetInvoiceItemId({Put your id}).SetItemDescription("{put your description}").SetPrice({Put your price}).SetQuantity({Put your quantity}).Build()
                    })
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    .Build();
billingService.ReduceInvoice(reduceInvoiceVo, response => Listener.GetResult(response, out output));

```


### دریافت لینک دانلود فایل های اکسل
جهت مشاهده وضعیت هریک از سرویس های درخواست داده شده خود برای دریافت فایل خروجی فاکتورها  میتوانید از سرویس
زیر استفاده نمایید.
در صورتی که وضعیت سرویس موفقیت آمیز بوده باشد از طریق تابع GetLink  میتوانید به لینک فایل ایجاد شده توسط سیستم دسترسی داشته باشید.مقادیر hashCode و fileId را پس از دریافت از سرویس GetExportList در تابع GetLink جایگذاری نمایید.

```
var output = new ResultSrv<List<ExportServiceSrv>>();
var getExportListVo = GetExportListVo.ConcreteBuilder
                    .SetOffset({Put your Offset})
                    //.SetSize({Put your Size})
                    //.SetId({Put your Id})
                    //.SetStatusCode({Put your StatusCode})
                    //.SetServiceUrl("{Put your ServiceUrl}")
                    .Build();
billingService.GetExportList(getExportListVo, response => Listener.GetResult(response, out output));
var link=getExportListVo.GetLink({Put your FileId}, "{Put your HashCode}");
```

### پرداخت فاکتور خارج از پلتفرم پاد
در صورتی که فاکتور به هر شکلی بجز امکانات موجود در پلتفرم پادپرداخت شد، میتوانید با استفاده از سرویس زیر، وضعیت آن را به حالت پرداخت شده ببرید. در این روش هیچ گونه سند مالی در پلتفرم ثبت نشده و به اعتبار افزوده نمی شود. دقت نمایید که کسب و کار فقط می تواند فاکتورهایی که خودش صادر نموده را با این روش پرداخت کند.

```
var output = new ResultSrv<bool>();
var payInvoiceVo = PayInvoiceVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    .Build();
billingService.PayInvoice(payInvoiceVo, response => Listener.GetResult(response, out output));

```

### پرداخت فاکتور با کیف پول از طریق پیامک
در صورتی که کاربر به رایانه جهت پرداخت دسترسی ندارد، یا در فروش حضوری، کسب و کار میتواند درخواست ارسال پیامک
پرداخت به کاربر دهد و کاربر با پیامک کردن کدی که دریافت کرده به همان شماره، فاکتور را از کیف پول خود پرداخت مینماید.

```
var output = new ResultSrv<bool>();
var sendInvoicePaymentSmsVo = SendInvoicePaymentSmsVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    //.SetWallet("{Put your Wallet}")
                    //.SetCallbackUri("Put your CallbackUri")
                    //.SetRedirectUri("Put your RedirectUri")
                    //.SetDelegationId({Put your DelegationId})
                    //.SetForceDelegation({Put your ForceDelegation})
                    .Build();
billingService.SendInvoicePaymentSms(sendInvoicePaymentSmsVo,response => Listener.GetResult(response, out output));

```


### پرداخت فاکتور در آینده
از طریق این سرویس کسب و کار قادر خواهد بود فاکتورهایی که برایش توسط دیگران صادر شده را درتاریخ آینده یا سررسید توافقی از طریق مبلغی که در کیف پول یا اصناف خود دارد  پرداخت نماید.
این سرویس باید توسط کسب و کار یا کاربر بدهکار یا شخصی که فاکتور برایش صادر شده صدا زده شود در غیر این صورت با خطای "فاکتور برای شما صادر نشده است" روبرو خواهد شد.

```
var output = new ResultSrv<bool>();
var ottOutput = GetOtt();
var payInvoiceInFutureVo = PayInvoiceInFutureVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    .SetDate("{Put your Date}")
                    .SetOtt(ottOutput.Ott)
                    //.SetGuildCode("{Put your GuildCode}")
                    //.SetWallet("{Put your Wallet}")
                    .Build();
billingService.PayInvoiceInFuture(payInvoiceInFutureVo,response => Listener.GetResult(response, out output));
```


### پرداخت فاکتور از طریق فاکتور
از طریق این سرویس کسب و کار قادر خواهد بود که پرداخت شدن برخی فاکتورهای خود را منوط به پرداخت شدن فاکتورهای دیگری
نماید. یا به عبارتی نوعی تهاتر را بوسیله فاکتورها انجام دهد که این امر توسط سرویس زیر قابل اجرا خواهد بود.

```
var output = new ResultSrv<bool>();
var payInvoiceByInvoiceVo = PayInvoiceByInvoiceVo.ConcreteBuilder
                    .SetCreditorInvoiceId({Put your CreditorInvoiceId})
                    .SetDebtorInvoiceId({Put your DebtorInvoiceId})
                    .Build();
billingService.PayInvoiceByInvoice(payInvoiceByInvoiceVo,response => Listener.GetResult(response, out output));

```


### نمایش پیش فاکتور

در پلتفرم کسب و کار، فاکتورهایی که پرداخت می شوند به صورت سالانه شماره سریال دریافت می نمایند، بنابرین کسب و کار می
تواند برای امور مالی خود به آن شماره سریال استناد نماید. در برخی شرایط، ممکن است کسب و کار بخواهد فاکتور تا زمانی که اقدام به پرداخت آن نشده اصلاً ثبت نگردد. بدین منظور با استفاده از سرویس زیر می تواند پیش فاکتور را ثبت نماید و با لینک بعدی آن را نمایش دهد. به محض اینکه مشتری، فاکتور را با کیف پول خود پرداخت نماید یا برای پرداخت وارد درگاه بانکی شود، فاکتور ثبت می گردد. در صورتی که مشتری پرداخت را از طریق درگاه لغو نماید یا اشکالی در پرداخت او به وجود آید، فاکتور به صورت خودکار لغو خواهد شد. 
دریافت می نمایید .
در پاسخ درخواست سرویس CreatePreInvoice یک کد hash دریافت می نمایید که  باید از طریق  ()createPreInvoiceVo.GetLink لینک را دریافت کرده و کاربر  را به آن آدرس هدایت کنید.

```
var output = new ResultSrv<string>();
var ottOutput = GetOtt();
var createPreInvoiceVo = CreatePreInvoiceVo.ConcreteBuilder
                    .SetToken({Put your ApiToken})
                    .SetOtt(ottOutput.Ott)
                    .SetProductsInfo(new List<ProductInfo>
                    {
                        ProductInfo.ConcreteBuilder.SetProductId({Put your ProductId}).SetPrice({Put your Price}).SetQuantity({Put your Quantity}).SetProductDescription("{Put your ProductDescription}").Build(),
                        ProductInfo.ConcreteBuilder.SetProductId({Put your ProductId}).SetPrice({Put your Price}).SetQuantity({Put your Quantity}).SetProductDescription("{Put your ProductDescription}").Build()
                    })
                    .SetGuildCode("{Put your GuildCode}")
                    .SetRedirectUri("{Put your RedirectUri}")
                    .SetUserId({Put your UserId})
                    //.SetBillNumber("{Put your BillNumber}")
                    //.SetCallUrl("{Put your CallUrl}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetDeadline("{Put your Deadline}")
                    //.SetDescription("{Put your Description}")
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    //.SetRedirectUri("{Put your RedirectUri}")
                    //.SetVerificationNeeded({Put your VerificationNeeded})
                    .Build();
billingService.CreatePreInvoice(createPreInvoiceVo,response => Listener.GetResult(response, out output));
var linkSrv = createPreInvoiceVo.GetLink(output.Result);


```

### پرداخت از کیف پول با ورود به SSO

مشتری برای مشاهده فاکتور خود و پرداخت آن از طریق کیف پول خود، لازم است از طریق آدرسی که تابع ()payInvoiceByWalletVo.GetLink  بعنوان خروجی می دهد هدایت شود.
مقدار invoiceId، مقداری است که از پاسخ سرویس issueInvoice با عنوان id  دریافت می‌نمایید و این مقدار از billNumber که توسط خود کسب و کار انتخاب  شده است، متمایز می‌باشد.
در این حالت، مشتری باید لاگین باشد و در صورتی که شناسه اشتباه وارد شود با خطای " فاکتور یافت نشد " مواجه می شود.
```
 var payInvoiceByWalletVo = PayInvoiceByWalletVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    //.SetCallUri("{Put your CallUri}")
                    //.SetRedirectUri("{Put your RedirectUri}")
                    .Build();
var output = payInvoiceByWalletVo.GetLink();

```

### دریافت لینک پرداخت 
ممکن است لازم باشد لینک پرداخت برای مشتری با روش های مختلفی ارسال شود. این لینک قابل اشتراک گذاری خواهد بود و هر کسی که آن را داشته باشد می تواند آن را پرداخت نماید. برای دریافت لینک از سرویسGetInvoicePaymentLink استفاده نمایید.
در پاسخ سرویس فوق یک لینک دریافت خواهید کرد که در صورت تمایل، می‌توانید  پارامترهای redirectUri ، callbackUri و "gateway="PEP را به تایع ()getInvoicePaymentLinkVo.GetAdvanceLink ارسال نمایید و لینک خود را دریافت نمایید. اگر پارامتر "gateway="PEP را  بگذارید، لینک تولید شده کاربر را مستقیما به صفحه درگاه پرداخت بانک  پاسارگاد هدایت خواهد شد و در صورت ارسال پارامتر redirectUri کاربر ملزم  به تکمیل فرآیند خرید، خواهد بود. 
توجه داشته باشید که لینک فوق، شامل یک هش کد می‌باشد که مدت اعتبار آن 300 ثانیه می‌باشد؛لذا در صورتی که با پیغام خطای " کد وارد شده معتبر نمی‌باشد و یا منقضی شده است." روبه‌رو شدید ممکن است کد هش منقضی شده باشد.

```
var output = new ResultSrv<string>();
var getInvoicePaymentLinkVo = GetInvoicePaymentLinkVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    .Build();
billingService.GetInvoicePaymentLink(getInvoicePaymentLinkVo,response => Listener.GetResult(response, out output));
var advanceLink = getInvoicePaymentLinkVo.GetAdvanceLink(output.Result, "PEP");

```


###پرداخت پیشرفته 
کسب و کار میتواند برای تمام مشتریان خود، بدون نیاز به ورود به سامانه احراز هویت یکپارچه، امکان خرید را از طریق لینک ()payInvoiceByUniqueNumberVo.GetLink  فراهم کند. برای این منظور لازم است کسب و کار از کد یکتا که برای فاکتور تولید می شود استفاده نماید. مراحل انجام کار به ترتیب:

1. ثبت نام کسب و کار در
https://services.pod.land

2. دریافت توکن جهت فراخوانی سرویس ها

3. ثبت فاکتور : دقت نمایید در صورت تمایل به نمایش شماره کارت های مربوط به  مشتری، در صفحه درگاه ضروری است شناسه کاربر (userId) در فاکتور ثبت شود.  این شناسه پس از ورود کاربر از طریق SSO بدست آمده یا می تواند شناسه ی  کاربر آفلاین (غیر SSO) باشد. در صورتی که شماره موبایل مربوط به هیچکدام  از این دودسته نیست، می توان با ثبت شماره موبایل (cellphoneNumber) در فاکتور، همین نتیجه را دریافت نمود.

4.  هدایت کاربر به درگاه ( از طریق  ()payInvoiceByUniqueNumberVo.GetLink لینک را دریافت نمایید )

5. تایید پرداخت

6.بستن فاکتور

7. تسویه

پارامتر redirectUri آدرسی است که بعد از پرداخت کاربر به آن هدایت می  گردد، پارامتر callUri نیز آدرسی در سرور شما میتواند باشد که در صورت موفق بودن پرداخت فراخوانی می گردد. پس از پرداخت پارمترهای زیر به صورت GET به  آدرس redirectUri برگردانده می شود. توجه: در صورتی که پارامتر gateway ارسال شود کاربر مستقیم به درگاه پرداخت بانک پاسارگاد متنقل می گردد. اگر مقدار uniqueNumber اشتباه ارسال شود، به صفحه "صفحه یافت نشد" هدایت می شوید.

```
var payInvoiceByUniqueNumberVo = PayInvoiceByUniqueNumberVo.ConcreteBuilder
                    .SetUniqueNumber("{Put your UniqueNumber}")
                    //.SetGateway("{Put your Gateway}")
                    //.SetRedirectUri("{Put your RedirectUri}")
                    //.SetCallUri("{Put your CallUri}")
                    .Build();
var output = payInvoiceByUniqueNumberVo.GetLink();

```


### تسویه از حساب مشتری (برداشت از کیف پول)
کسب و کار می تواند از طریق سرویس RequestSettlement  و ایجاد نمونه از کلاس RequestWalletSettlementVo ،
مبلغ مورد نظر خود را از کیف پولش به شماره شبای ثبت شده در پروفایل خود منتقل کند. در صورتی که شماره شبا یا نام و نام خانوادگی شخص در پروفایل ثبت نشده باشد این سرویس خطا خواهد داد. کد ارز شامل کد سه حرفی رایج برای واحدهای پولی است. مانند
IRR و USD

```
var ottOutput = GetOtt();
var output = new ResultSrv<SettlementRequestSrv>();
var requestWalletSettlementVo= RequestWalletSettlementVo.ConcreteBuilder
                    .SetAmount({Put your Amount})
                    .SetOtt(ottOutput.Ott)
                    //.SetWallet("{Put your Wallet}")
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetSheba("{Put your Sheba}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetUniqueId("{Put your UniqueId}")
                    //.SetDescription("{Put your Description}")
                    .Build();
billingService.RequestSettlement(requestWalletSettlementVo, response => Listener.GetResult(response, out output));

```


### تسویه از حساب صنفی کسب و کار
در حساب های صنفی همواره مبلغی به عنوان مبلغ قابل تسویه وجود دارد که شامل دارایی کسب و کار بجز فاکتورهای باز او یا فاکتورهایی که مبلغ آن ها هنوز واریز نشده است، می باشد. مبلغ قابل تسویه را می توان از طریق RequestSettlement و ایجاد نمونه از کلاس RequestGuildSettlementVo تسویه نمود. کد ارز شامل کد سه حرفی رایج برای واحدهای پولی است. مانند
IRR و USD

```
var ottOutput = GetOtt();
var output = new ResultSrv<SettlementRequestSrv>();
var requestGuildSettlementVo= RequestGuildSettlementVo.ConcreteBuilder
                    .SetGuildCode("{Put your GuildCode}")
                    .SetAmount({Put your Amount})
                    .SetOtt(ottOutput.Ott)
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetSheba("{Put your Sheba}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetUniqueId("{Put your UniqueId}")
                    //.SetDescription("{Put your Description}")
                    .Build();
billingService.RequestSettlement(requestGuildSettlementVo,response => Listener.GetResult(response, out output));

```


###انتقال وجه از حساب کسب و کاری به کارت بانکی (با کسر کارمزد) یا شماره شبا
کسب و کار می تواند با استفاده از سرویس زیر مبلغ مورد نظر خود را از حساب مجازی به یک شماره کارت یا یک شماره شبا بانکی منتقل نماید. بدیهی است که در صورت استفاده از ابزار کارت به کار، کارمزد بانکی از حساب کسب و کار کسر خواهد شد و در صورت استفاده از ابزار پایا، انتقال وجه در زمان مصوب بانک مرکزی انجام خواهد شد. برای پارامتر toolCode از یکی از مقادیر زیر استفاده نمایید:
SETTLEMENT_TOOL_SATNA
SETTLEMENT_TOOL_PAYA
SETTLEMENT_TOOL_CARD
   و به طور مثال، در صورتی که انتقال از طریق کارت را انتخاب نموده اید، در قسمت toolId شماره کارت مقصد را وارد نمایید و در غیر این صورت شماره شبا را وارد نمایید. کد ارز شامل کد سه حرفی رایج برای واحدهای پولی است. مانند IRR و USD

```
var ottOutput = GetOtt();
var output = new ResultSrv<SettlementRequestSrv>();
var requestSettlementByToolVo = RequestSettlementByToolVo.ConcreteBuilder
                    .SetToolCode({Put your ToolCode})
                    .SetToolId("{Put your ToolId}")
                    .SetAmount("{Put your Amount}")
                    .SetGuildCode("{Put your GuildCode}")
                    .SetOtt(ottOutput.Ott)
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetUniqueId("{Put your UniqueId}")
                    //.SetDescription("{Put your Description}")
                    .Build();
billingService.RequestSettlement(requestSettlementByToolVo,response => Listener.GetResult(response, out output));

```

### گزارش وضعیت تسویه
جهت دریافت لیست تسویه ها و وضعیت آن ها از سرویس ListSettlements استفاده نمایید.
```
var output = new ResultSrv<List<SettlementRequestSrv>>();
var listSettlementsVo = ListSettlementsVo.ConcreteBuilder
                    .SetOffset({Put your Offset})                    
                    //.SetSize({Put your Size})
                    //.SetStatusCode({Put your StatusCode})
                    //.SetFromAmount({Put your FromAmount})
                    //.SetToAmount({Put your ToAmount})
                    //.SetFromDate("{Put your FromDate}")
                    //.SetToDate({Put your ToDate})
                    //.SetUniqueId("{Put your UniqueId}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    .Build();
billingService.ListSettlements(listSettlementsVo, response => Listener.GetResult(response, out output));

```

###فعالسازی تسویه خودکار در صورتی
که تسویه خودکار برای یک کسب و کارفعال شود، مبلغ قابل تسویه آن کسب و کار به طور خودکار، یکبار در شبانه روز به شماره شبای اعلام شده در پروفایل کسب و کار یا شماره شبای اعلامی در سرویس زیر، تسویه می گردد. برای فعالسازی تسویه خودکار سرویس زیر را با توکن کسب و کار دارنده حساب فراخوانی نمایید.

```
var ottOutput = GetOtt();
var output = new ResultSrv<bool>();
var addAutoSettlementVo = AddAutoSettlementVo.ConcreteBuilder
                    .SetGuildCode("{Put your GuildCode}")
                    .SetOtt(ottOutput.Ott)
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetSheba("{Put your Sheba}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetInstant({Put your Instant})
                    .Build();
billingService.AddAutoSettlement(addAutoSettlementVo,response => Listener.GetResult(response, out output));

```


### لغو تسویه خودکار
با سرویس زیر می‌توانید تسویه خودکار را غیرفعال نمایید.

```
var output = new ResultSrv<bool>();
var registerUserVo = RemoveAutoSettlementVo.ConcreteBuilder
                    .SetGuildCode("{Put your GuildCode}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    .Build();
billingService.RemoveAutoSettlement(registerUserVo,response => Listener.GetResult(response, out output));

```


### اجازه ثبت فاکتور
در صورتی که بخشی از فروش شما به کسب و کار دیگری تعلق دارد و میخواهید فاکتور به نام همان کسب و کار ثبت شود، لازم است آن کسب و کار به کسب و کار شما اجازه صدور فاکتور به عنوان معامله گر را داده باشد. برای این منظور خود کسب و کار ذینفع یا کارگزار او، با استفاده از توکن که در اختیار دارد، با استفاده از سرویس زیر به کسب کار دیگر اجازه صدور فاکتور می دهد.

```
var output = new ResultSrv<BusinessDealerSrv>();
var addDealerVo = AddDealerVo.ConcreteBuilder
                    .SetDealerBizId({Put your DealerBizId})
                    //.SetAllProductAllow({Put your AllProductAllow})
                    .Build();
billingService.AddDealer(addDealerVo, response => Listener.GetResult(response, out output));

```

### دریافت لیست کسب و کارها

برای دریافت یا جستجوی لیست تمام کسب و کارهایی که به آنها مجوز معامله و صدور فاکتور داده اید، از سرویس زیر استفاده نمایید.
توجه داشته باشید در صورتی که شناسه کسب و کار را اشتباه وارد کنید، با اررور "شناسه کسب و کار یافت نشد" مواجه نخواهید شد بلکه در فایل خروجی هیچ مقداری دریافت نخواهید کرد.
(با hasError": false")
```
var output = new ResultSrv<List<BusinessDealerSrv>>();
var dealerListVo = DealerListVo.ConcreteBuilder
                    //.SetDealerBizId(0)
                    //.SetEnable(false)
                    //.SetOffset(0)
                    //.SetSize(0)
                    .Build();
billingService.DealerList(dealerListVo, response => Listener.GetResult(response, out output));
```


### فعالسازی مجوز معامله گران
برای فعالسازی مجوز معامله گران، به ترتیب از سرویس  زیر استفاده نمایید.

```
var output = new ResultSrv<BusinessDealerSrv>();
 var enableDealerVo = EnableDealerVo.ConcreteBuilder
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.EnableDealer(enableDealerVo, response => Listener.GetResult(response, out output));

```

### فعالسازی مجوز معامله گران
برای غیر فعالسازی مجوز معامله گران، از سرویس  زیر استفاده نمایید.

```
var output = new ResultSrv<BusinessDealerSrv>();
 var enableDealerVo = EnableDealerVo.ConcreteBuilder
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.EnableDealer(enableDealerVo, response => Listener.GetResult(response, out output));
```

### لیست کسب و کارهایی که واسط آن هستید
با فراخوانی سرویس زیر می توانید لیست کسب و کارهایی که واسط آن ها شده اید را دریافت نمایید.

```
var output = new ResultSrv<List<BusinessDealerSrv>>();
var businessDealingListVo = BusinessDealingListVo.ConcreteBuilder
                    .SetDealerBizId({Put your DealerBizId})
                    //.SetEnable({Put your Enable})
                    //.SetOffset({Put your Offset})
                    //.SetSize({Put your Size})
                    .Build();
billingService.BusinessDealingList(businessDealingListVo,response => Listener.GetResult(response, out output));

```

### صدور فاکتور تسهیمی
کسب و کار معامله گر که لازم است فاکتور تسهیمی صادر نماید باید از جانب کسب و کارهای سهیم دارای مجوز صدور فاکتور باشد. سپس می‌تواند با استفاده از سرویس زیر تسهیم فروش انجام دهد.

```
var output = new ResultSrv<InvoiceSrv>();
var ottOutput = GetOtt();
var mainInvoiceVos = MainInvoiceVo.ConcreteBuilder
                    .SetGuildCode("{Put your GuildCode}")
                    .SetInvoiceItemVOs(new List<InvoiceItemVo>
                    {
                        InvoiceItemVo.ConcreteBuilder.SetProductId({Put your ProductId}).SetDescription("{Put your 
                        Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                    })
                    //.SetBillNumber("{Put your BillNumber}")
                    //.SetDescription("{Put your Description}")
                    //.SetMetadata("{Put your Metadata}")
                    .Build();
                  
var subInvoiceVos = new List<SubInvoiceVo>
                {
                    SubInvoiceVo.ConcreteBuilder
                        .SetBusinessId({Put your BusinessId})
                        .SetGuildCode("{Put your GuildCode}")
                        .SetInvoiceItemVOs(new List<InvoiceItemVo>
                        {
                            InvoiceItemVo.ConcreteBuilder.SetProductId({Put your ProductId}).SetDescription("{Put your 
                            Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                        })
                        //.SetBillNumber("{Put your BillNumber}")
                        .SetDescription("{Put your Description}")
                        //.SetMetadata("{Put your Metadata}")
                        .Build()
                   
                };
var customerInvoiceItems = new List<InvoiceItemVo>
                {
                    InvoiceItemVo.ConcreteBuilder.SetProductId({Put your ProductId}).SetDescription("{Put your 
                            Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                };
                var multiInvoiceData = MultiInvoiceDataVo.ConcreteBuilder
                    .SetMainInvoice(mainInvoiceVos)
                    .SetSubInvoices(subInvoiceVos)
                    .SetCustomerInvoiceItemVOs(customerInvoiceItems)
                    //.SetPreview({Put your Preview})
                    //.SetCurrencyCode("Put your CurrencyCode")
                    //.SetCustomerDescription("{Put your CustomerDescription}")
                    //.SetCustomerMetadata("{Put your CustomerMetadata}")
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    //.SetRedirectUrl("{Put your RedirectUrl}")
                    //.SetUserId({Put your UserId})
                    //.SetVerificationNeeded({Put your VerificationNeeded})
                    //.SetVoucherHashs({Put your VoucherHashs})
                    .Build();

var issueMultiInvoiceVo = IssueMultiInvoiceVo.ConcreteBuilder
                    .SetOtt(ottOutput.Ott)
                    .SetData(multiInvoiceData)
                    //.SetDelegationHash("{Put your DelegationHash}")
                    //.SetDelegatorId("{Put your DelegatorId}")
                    //.SetForceDelegation("{Put your ForceDelegatio}")
                    .Build();
billingService.IssueMultiInvoice(issueMultiInvoiceVo, response => Listener.GetResult(response, out output));

```


### کاهش فاکتور تسهیمی
در فاکتور تسهیمی نیز مانند فاکتور عادی با لغو شدن، کل مبلغ فاکتور و با کاهش، قسمتی از مبلغ به مشتری بازگردانده می شود. ولی در فاکتور تسهیمی برای کاهش لازم است کل سهم ها مجدداً اعلام شوند تا مبلغی که کسر می شود از حساب درست برداشته شود. برای کاهش فاکتور تسهیمی از سرویس ReduceMultiInvoice استفاده نمایید.
مقدار id در تمام بخش های اطلاعات ارسالی باید مطابق با شناسه های فاکتور اصلی باشد، در غیر این صورت خطا رخ می دهد. در فاکتور اصلاح شده نیز شرایط زیر لازم است برقرار باشد:      
the share of dealer + the share of shareholder =  the price to be payed by customer
```
 var output = new ResultSrv<InvoiceSrv>();
var mainInvoiceVos = ReduceInvoiceItemVo.ConcreteBuilder
                    .SetId({Put your Id})
                    .SetReduceInvoiceItemVOs(new List<ReduceInvoiceSubItemVo>
                    {
                        ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                    })
                    .Build();

var subInvoiceVos = new List<ReduceInvoiceItemVo>
                {
                    ReduceInvoiceItemVo.ConcreteBuilder
                        .SetId({Put your Id})
                        .SetReduceInvoiceItemVOs(new List<ReduceInvoiceSubItemVo>
                        {
                            ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your 
                            Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                        })
                        .Build()
                };
                var customerInvoiceItems = new List<ReduceInvoiceSubItemVo>
                {
                    ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity})
                        .Build()
                };

var reduceMultiInvoiceDataVo = ReduceMultiInvoiceDataVo.ConcreteBuilder
                    .SetMainInvoice(mainInvoiceVos)
                    .SetSubInvoices(subInvoiceVos)
                    .SetCustomerInvoiceItemVOs(customerInvoiceItems)
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    .Build();

var reduceMultiInvoiceVo = ReduceMultiInvoiceVo.ConcreteBuilder
                    .SetData(reduceMultiInvoiceDataVo)
                    .Build();
billingService.ReduceMultiInvoice(reduceMultiInvoiceVo, response => Listener.GetResult(response, out output));

```

### کاهش فاکتور تسهیمی و انتقال به شبا
در صورتی که می خواهید بلافاصله بعد از کاهش فاکتور، مبلغ برگشتی به شماره شبا کاربر منتقل گردد، از سرویس زیر با همان فرمت data سرویس ReduceMultiInvoice، استفاده نمایید.

```
var output = new ResultSrv<InvoiceSrv>();
var mainInvoiceVos = ReduceInvoiceItemVo.ConcreteBuilder
                    .SetId({Put your Id})
                    .SetReduceInvoiceItemVOs(new List<ReduceInvoiceSubItemVo>
                    {
                        ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your 
                        Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                    })
                    .Build();

var subInvoiceVos = new List<ReduceInvoiceItemVo>
                {
                    ReduceInvoiceItemVo.ConcreteBuilder
                        .SetId({Put your Id})
                        .SetReduceInvoiceItemVOs(new List<ReduceInvoiceSubItemVo>
                        {
                            ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your Description}").SetPrice(50)
                                .SetQuantity({Put your Quantity}).Build()
                        })
                        .Build()
                };
                var customerInvoiceItems = new List<ReduceInvoiceSubItemVo>
                {
                    ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your 
                    Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                };

var reduceMultiInvoiceDataVo = ReduceMultiInvoiceDataVo.ConcreteBuilder
                    .SetMainInvoice(mainInvoiceVos)
                    .SetSubInvoices(subInvoiceVos)
                    .SetCustomerInvoiceItemVOs(customerInvoiceItems)
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    .Build();

var reduceMultiInvoiceAndCashoutVo = ReduceMultiInvoiceAndCashoutVo.ConcreteBuilder
                    .SetData(reduceMultiInvoiceDataVo)
                    .SetToolCode({Put your ToolCode})
                    .Build();
billingService.ReduceMultiInvoiceAndCashout(reduceMultiInvoiceAndCashoutVo, response => Listener.GetResult(response, out output));

```


### مجوز فروش محصول
همانطور که توضیح داده شد، به منظور صدور فاکتور تسهیمی (در صورت شراکت با یک کسب و کار دیگر)، فراخوانی سرویس nzh/biz/addDealer قبل از فراخوانی سرویس صدور فاکتور تسهیمی، الزامی ست. اما در صورتی که برای یک محصول خاص، بخواهید به کسب و کار دیگری مجوز صدور فاکتور عادی اعطا کنید، علاوه بر فراخوانی سرویس ذیل، باید سرویس nzh/biz/addDealer را نیز فراخوانی نمایید و سپس سرویس صدور فاکتور(nzh/issueInvoice) را  فراخوانی نمایید؛ در غیر این صورت با خطای  "کسب و کار دلال وارد شده دلال  کسب و کار مالک محصول نمی باشد" مواجه خواهید شد.
شناسه محصول(EntityId) و شناسه کسب و کار(DealerBizId) را کافی ست در در  کلاس AddDealerProductPermissionVo مقداردهی نمایید و سپس سرویس AddDealerProductPermission فراخوانی کنید.

```
var output = new ResultSrv<DealerProductPermissionSrv>();
var registerUserVo = AddDealerProductPermissionVo.ConcreteBuilder
                    .SetEntityId({Put your EntityId})
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.AddDealerProductPermission(registerUserVo, response => Listener.GetResult(response, out output));

```

### دریافت لیست مجوزها
با این سرویس می توانید لیست مجوزهای خود به کسب و کارهای واسط دیگر را به انضمام شناسه محصول، مشاهده نمایید.

```
var output = new ResultSrv<List<DealerProductPermissionSrv>>();
var registerUserVo = DealerProductPermissionListVo.ConcreteBuilder
                    //.SetSize({Put your Size})
                    //.SetDealingBusinessId({Put your DealingBusinessId})
                    //.SetEnable({Put your Enable})
                    //.SetOffset({Put your Offset})
                    //.SetEntityId({Put your EntityId})
                    .Build();
billingService.DealerProductPermissionList(registerUserVo,response => Listener.GetResult(response, out output));

```

### لیست مجوزهای صادر شده برای کسب و کار شما
لیست دسترسی هایی که شما واسط آن کسب و کار شده اید و برای آن محصول خاص مجوز صدور فاکتور گرفته اید را می توانید با سرویس
زیر مشاهده نمایید.

```
var output = new ResultSrv<List<DealerProductPermissionSrv>>();
var registerUserVo = DealingProductPermissionListVo.ConcreteBuilder
                    //.SetSize({Put your Size})
                    //.SetDealingBusinessId({Put your DealingBusinessId})
                    //.SetEnable({Put your Enable})
                    //.SetOffset({Put your Offset})
                    //.SetEntityId({Put your EntityId})
                    .Build();
billingService.DealingProductPermissionList(registerUserVo,response => Listener.GetResult(response, out output));
                
                

```


### فعال کردن دسترسی محصول
با استفاده از سرویس ذیل می توانید دسترسی محصولی به کسب و کار واسط اعطا نموده اید را فعال نمایید.

```
var output = new ResultSrv<DealerProductPermissionSrv>();
var enableDealerProductPermissionVo= EnableDealerProductPermissionVo.ConcreteBuilder
                    .SetEntityId({Put your EntityId})
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.EnableDealerProductPermission(enableDealerProductPermissionVo,response => Listener.GetResult(response, out output));
```

### غیرفعال کردن دسترسی محصول
 با استفاده از سرویس ذیل می توانید دسترسی محصولی که به کسب و کار واسط اعطا نموده اید را غیرفعال نمایید.

```
var output = new ResultSrv<DealerProductPermissionSrv>();
var registerUserVo = DisableDealerProductPermissionVo.ConcreteBuilder
                    .SetEntityId({Put your EntityId})
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.DisableDealerProductPermission(registerUserVo,response => Listener.GetResult(response, out output));
```

<div class="box-end">
</div>
## گزارش‌گیری

با استفاده از این سرویس و اطلاعاتی که از پرداختی‌های خود دارید، می‌توانید گزارش‌های دقیق و کاملی از فرآیند مالی کسب‌وکارتان به‌دست آورید.
<div class="box-end">
</div>

## لاماسو

این سرویس، اتاق‌های قابل رزرو هتل‌ها و نرخ‌‌های ارائه‌شده برای هر کدام را مستقیماً برای آژانس‌های مسافرتی و مراکز رزرو دهنده آنلاین، به‌روزرسانی می‌کند. با این کار، رزرو اتاق به آسانی و با سرعت و دقت بیشتری صورت می‌گیرد و از بروز مشکلاتی مثل پذیرش بیش از ظرفیت جلوگیری می‌شود.
هتل‌ها و مراکز اقامتی با استفاده از این سرویس، می‌توانند به مراکز رزرودهنده و آژانس‌های مسافرتی متصل شوند. این سرویس زیرساختی برای ارائه‌ی اطلاعات هتل‌ها به صورت یک‌پارچه است تا کارگزاران و فروشندگان بتوانند اطلاعات هتل‌های خود را به رزرو کننده‌های زیادی ارائه کنند.

## دریافت شهرها

این متد برای دریافت لیست جست و جوی شهر‌های ثبت شده در سیستم و برای استفاده‌های آتی قابل استفاده است.

لازم به ذکر است با توجه به عدم ثبت همه شهرهای ایران با کد استاندارد جهانی، شهرهایی که کد IATA داشته اند از همان استفاده شده است.

    HEADER:
        Authorization=[api-key]
    Method:
        GET
    Url:
        [base-url]/booking/cities
        شماره محصول برای فراخوانی به صورت سرویس کال: productId = 10707

+ **توجه:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Authorization نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحات زیر ارسال نمائید:

نحوه استفاده از سرویس کال پاد

## دریافت قوانین

در این متد سیاست‌های فروش و محدودیت های فروش و شرایط قراردادی برای هتل‌ها برای شما ارسال خواهد شد.

    HEADER:
        Authorization=[api-key]
    Method:
        GET
    Url:
        [base-url]/booking/policies

شماره محصول برای فراخوانی به صورت سرویس کال: productId = xxxxx

+ **توجه:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Authorization نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحات زیر ارسال نمائید:

نحوه استفاده از سرویس کال پاد

## دریافت امکانات

این متد با هدف ایجاد جدول جست و جو برای سامانه مشتری قرار گرفته است. برای دریافت این اطلاعات تنها نیاز است به آدرس مورد نظر درخواست ارسال شود. در پاسخ برای شما مجموعه‌ای از امینیتی‌ها ارسال خواهد شد که شامل نام و شناسه و نوع خواهد بود.نوع نشان دهنده این است که این امینیتی مربوط به هتل بوده یا اتاق.

    HEADER:
        Authorization=[api-key]
    Method:
        GET
    Url:
        [base-url]/booking/amenities

شماره محصول برای فراخوانی به صورت سرویس کال: productId = 10706

+ **توجه 1:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Authorization نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحات نحوه استفاده از سرویس کال پاد ارسال نمائید.
+ **توجه 2:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، مقدار هر یک از پارامترهای فوق را با استفاده از paramNames و paramValues ارسال نمائید. 

## دریافت اطلاعات اولیه هتل‌ها

این متود برای دریافت لیست هتل ها و جزییات مربوط به هرکدام از آنها استفاده میشود لیست مربوط به هتل ها با توجه  به apiKey مربوط به آژانس مورد نظر 

    HEADER:
            Authorization = [api-key]
    Method: GET
    Url:
            [base-url]/booking/hotel_inventory

شماره محصول برای فراخوانی به صورت سرویس کال: productId = 10705

## موجودی هتل

با استفاده از این روش و با وارد کردن آی دی هتل و تاریخ ورود و تاریخ خروج موجودی هتل نمایش داده خواهد شد.

در این روش می‌توان اطلاعات بیش از یک هتل را درخواست کرد.

لازم به ذکر است در بدنه درخواست و در فیلد hotel_ids مجموعه شناسه‌ها باید در قالب یک آرایه ارسال گردند. 

پارامترها با ملاحظات زیر باید در بدنه درخواست قرار بگیرند:

    HEADER:
            Authorization= [api-key]
       
    Method: POST
    Url:
            [base-url]/booking/hotel_availability
    Parameters:
            hotel_ids=                   //hotel ids from https://api.lamasoo.com/docs/#/Static/HotelInventoryGet
            start_date=                 //check-in date for the reservation
            end_date=                  //check-out date for the reservation
            lang=                       //ISO 3166-1 alpha-2
            currency=                  //ISO 4217
            user_country=             //ISO 3166-1 alpha-2 country code.

شماره محصول برای فراخوانی به صورت سرویس کال: productId = 10710

+ **توجه 1:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Authorization نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحات نحوه استفاده از سرویس کال پاد ارسال نمائید.
+ **توجه 2:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، مقدار هر یک از پارامترهای فوق را با استفاده از paramNames و paramValues ارسال نمائید. 

## موجود بودن اتاق برای رزرو

با استفاده از متد اطلاعات موجودی یک هتل در یک تاریخ مشخص با جزئیات قیمت و نر‌خ‌نامه و ظرفیت و قیمت نفر اضافه بدست می‌آید. 

در این متد شناسه هتل نباید به صورت آرایه ارسال گردد. این متد تنها شناسه یک هتل را به عنوان ورودی دریافت می‌کند.

شناسه هتل مورد نظر باید از داده‌های Hotel_Inventory برداشته شود.

پارامترها با ملاحظات زیر باید در بدنه درخواست قرار بگیرند:

```
HEADER:
        Authorization= [api-key]

Method: POST
Url:
        [base-url]//booking/booking_availability
Parameters:
        hotel_id=                    //hotel id
        start_date=                 //check-in date for the reservation
        end_date=                  //check-out date for the reservation
        lang=                       //ISO 3166-1 alpha-2
        currency=                  //ISO 4217
        user_country=             //ISO 3166-1 alpha-2 country code.
```



شماره محصول برای فراخوانی به صورت سرویس کال: productId = 10711

+ **توجه 1:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Authorization نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحات نحوه استفاده از سرویس کال پاد ارسال نمائید.
+ **توجه 2:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، مقدار هر یک از پارامترهای فوق را با استفاده از paramNames و paramValues ارسال نمائید. 

## ثبت اولیه رزرو

این متد برای ثبت رزرو اولیه و برای قفل کردن اتاق برای ثبت نهایی استفاده می‌شود. این متد ۱۵ دقیقه اتاق را در هتل قفل و برای شخصی که در این درخواست ارائه می‌شود در هتل محفوظ نگه‌ میدارد.

در این متد نکته مهم رفرنس آی-دی خواهد بود که رزرو کننده باید این کد را در بدنه درخواست ارسال نماید. این کد باید برای همان رزرو دهنده یکتا باشد و برای پیگیری های آتی قابل استفاده است.

در این درخواست نکته مهم ثبت آبجکت‌های رزرو مطابق مثال خواهد بود.

برای ثبت چند اتاق (از انواع متفاوت و یا از یک نوع) باید در آبجکت‌های مختلف و با تعیین تعداد نفرات بزرگسال و کودک در همان اتاق انجام پذیرد.

در صورت مغایرت حداکثر تعداد نفرات اضافه در هر اتاق با خطا مواجه خواهید شد. اطلاعات مربوط به ظرفیت و ظرفیت نفر اضافه و شناسه هتل و شناسه اتاق‌های هر اتاق در پاسخ متد booking availablity و یا hotels/hotel inventory به شما برخواهد گشت.

در این متد نام شخصی که برای ثبت رزرو در بدنه ارسال می‌شود در هتل ثبت خواهد شد.

تعداد کودک در هر اتاق باید به صورت یک آرایه از سن کودکان هر اتاق ثبت شود ولی تعداد نفرات بزرگسال در هر اتاق به صورت یک عدد قابل ثبت است.

در این متد rate_plan_id باید مانند موارد ظرفیت و شناسه هتل در پاسخ booking availablity برای رزرو دهنده ارسال شده است.

این آی دی برای هر هتل می‌تواند مقادیر متفاوتی داشته باشد. در بازه‌‌های زمانی متفاوت تغییر کند. این شناسه نشان‌دهنده نرخ‌نامه هر قیمت خواهد بود به طور مثال هتل برای آژانس الف نرخنامه تابستان را در دسترس قرار داده و مثلا آی دی این نرخنامه 1721 خواهد بود

این شناسه ممکن است به صورت عددی و یا ترکیبی از هر دو باشد.

در حال حاضر تناظری بین ‌‌شناسه های هتل های متفاوت وجود ندارد.

در انتها، بدنه این متد دارای ورودی payment_method است که از بین روش ‌‌های پرداخت مختلف ممکن برای رزرو دهنده حالت‌های متفاوتی ارائه شده.

در اکثر موارد متد پرداخت pod_credit باید استفاده شود که آی دی این متد : 5ac8dce63dbd6c97c69b3746 می باشد.

در پاسخ این متد به شما در صورت ثبت موفق رفرنس آی دی و مبلغ ثبت رزرو و شماره فاکتوری که باید توسط رزرو کننده در پاد پرداخت شود (توسط متد pay_invoice_by_id) که در پاد و وب‌سرویس‌های پاد در دسترس است.

و در صورت بروز خطا، خطای مربوطه به شما ارائه خواهد شد.

```
HEADER:
        Authorization= [api-key]
Method: POST
Url:
        [base-url]/booking/booking_submit/
Parameters:
        checkin_date=            //checkin date of passenger
        checkout_date=          //checkout date of passenger
        hotel_id=                  //hotel id from previous method's response
        reference_id=            //better generated by client side, if it is not sent by client it should generated by Lamasoo and  you receive it in response of submit
        payment_method=      //to pay by POD platform should set "5ac8dce63dbd6c97c69b3746"
        customer=
            first_name=                //first name of passenger or POD user
            last_name=                //last name of passenger or POD user
            national_code=            //national id of passenger or POD user
            phone_number=           //phone number of passenger or POD user
            country=                   //ISO 3166-1 alpha-2 country code and should be the passenger nationality
         rooms=                       
            type_id=                   //from booking_availablity method's response
            count=                     //number of each room type needed
            party=
```



شماره محصول برای فراخوانی به صورت سرویس کال: productId = 10712

+ **توجه 1:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Authorization نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحات نحوه استفاده از سرویس کال پاد ارسال نمائید.
+ **توجه 2:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، مقدار هر یک از پارامترهای فوق را با استفاده از paramNames و paramValues ارسال نمائید. 

## بررسی رزرو

این متد برای پیگیری‌های آتی قابل استفاده است.

برای استفاده از این متد باید کد رفرنسی که پیش از این در متد submit و confirm در فیلد refrence_id تبادل شده است و hotel_id ارسال شود.

در پاسخ وضعیت رزرو مورد درخواست در سه حالت ناشناخته و تایید شده و ناموفق به شما ارسال می‌شود.

درحالت ناشناخته به صورت کلی مشکل از refrence_id بوده‌است.

```
HEADER:
        Authorization= [api-key]

Method: POST
Url:
        [base-url]//booking/booking_verify
Parameters:
        hotel_id=                    // hotel id
        reference_id=              // reference_id should be the same value in the submit api
```



شماره محصول برای فراخوانی به صورت سرویس کال: productId = 10713

+ **توجه 1:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Authorization نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحات نحوه استفاده از سرویس کال پاد ارسال نمائید.
+ **توجه 2:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، مقدار هر یک از پارامترهای فوق را با استفاده از paramNames و paramValues ارسال نمائید. 

## تائید رزرو

بعد از استفاده از متد submit که رزرو را تا مدت معین محفوظ نگه‌ خواهد داشت، متد کانفرم بر اساس اطلاعاتی که در متد submit ارسال شده پردازش خواهد شد.

به طور مثال اگر متد پرداختی نقدی و یا از اعتبار پاد را در submit انتخاب کرده باشید باید قبل از کانفرم پرداخت انجام گرفته باشد و پس از آن می‌توانید با استفاده از refrence_id و hotel_id این متد را فراخوانی کنید. در پاسخ با توجه به این موارد برای شما ارسال می‌گردد.

لازم به ذکر است این متد در صورتی که بیش از زمان معین از ثبت اولیه (submit) گذشته باشد قابل استفاده نیست با خطا مواجه خواهد شد.`
``

    HEADER:
            Authorization =[api-key]
    
    Method: POST
    Url:
            [base-url]/booking/booking_confirm
    Parameters:
            hotel_id=              //hotel id
            reference_id=        //refrence id which used in booking submit method

`
شماره محصول برای فراخوانی به صورت سرویس کال: productId = 10714

+ **توجه 1:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، نیازی به ارسال هدر Authorization نیست و شما بایستی پارامتر serviceCallToken را مطابق توضیحات نحوه استفاده از سرویس کال پاد ارسال نمائید.
+ **توجه 2:** در فراخوانی متد فوق بصورت سرویس کال و از طریق پاد، مقدار هر یک از پارامترهای فوق را با استفاده از paramNames و paramValues ارسال نمائید. 

<div class="box-end">
</div>

## تقویم
با استفاده از این سرویس می‌توانید برای هر گردشگر یک تقویم ایجاد کنید و در آن با استفاده از تعریف رویداد، زمان دقیق برنامه‌هایی را که برایشان در نظر دارید مشخص کنید. 

### افزودن تقویم

نکته ای که در مورد افزودن تقویم وجود دارد این است که سیستم به صورت پیش فرض یک تقویم برای کاربر ایجاد میکند که این تقویم قابل حذف نیست . ایجاد تقویم پیش فرض به این صورت است که چنانچه تقویم مورد نظر اولین تقویم کاربرباشد به صورت سیستمی تقویم پیش فرض کاربر تلقی می‌شود.
برای اضافه نمودن تقویم از سرویس زیر استفاده نمایید:

    HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
            PUT
    Url:
            [platform-address]/nzh/addCalendar/
    Parameters:
            sharedPersons={"userIdentity":identity(username, chellphone or email) of user whom is one of 
            sharedPersons,"permissionTypeCode":one type of permissionTypeCode}
            sharedPersons={"userIdentity":identity(username, chellphone or email) of user whom is one of 
            sharedPersons,"permissionTypeCode":one type of permissionTypeCode}
            sharedPersons={"userIdentity":[identity(username, chellphone or email) of user whom is one of 
            sharedPersons],"permissionTypeCode":[one type of permissionTypeCode]}
            name=             //name of calendar
            longitude=
            latitude=

### ویرایش تقویم

به منظور ویرایش هر یک از فیلدهای موجود در سرویس اضافه کردن تقویم، فیلد مورد نیاز را به لیست پارامترها اضافه و سرویس را فراخوانی نمایید.

نکته قابل توجه در خصوص لیستها این است که با هر بار فراخوانی ویرایش میبایست تمام عناصر لیستها لحاظ شوند در غیر اینصورت مقادیر قبلی با مقادیر جدید جایگزین میگردند.

برای مثال اگر بخواهیم به افراد مشترک در تقویم علاوه بر فرد A و فرد B، فرد C را هم اضافه کنیم هر دو A, B را به اضافه C به لیست اضافه میکنیم. در غیر اینصورت اگر فقط C عضو لیست باشد، با عمل ویرایش تقویم دو عضو قبلی پاک شده و فقط فرد C به عنوان کاربر مشترک تقویم ثبت خواهد شد.

    HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
            PUT
    Url:
            [platform-address]/nzh/editCalendar/
    Parameters:
            sharedPersons={"userId":[id of user whom is one of sharedPersons],"permissionTypeCode":[one type of 
            permissionTypeCode]}
            id=[identifier of calendar]
            sharedPersons={"userIdentity ":[userIdentity(userName, chellphone or email) of user whom is one of 
            sharedPersons],"permissionTypeCode":[one type of permissionTypeCode]}
            sharedPersons={"userIdentity ":[userIdentity(userName, chellphone or email) of user whom is one of 
            sharedPersons],"permissionTypeCode":[one type of permissionTypeCode]}
            name=[name of calendar]

### لیست تقویم های من

جهت دریافت لیست تقویم هایی که صاحب آن کاربر جاری است.

نام سرویس : listMyCalendars

ورودی های سرویس : 

offset - شماره اولین عضو لیست

size -  تعداد عناصر

    HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
            PUT
    Url:
            [platform-address]/nzh/listMyCalendars/
    Parameters:
            _token_=[user token]
            _token_issuer_=1
           offset=[offset of result list]
           size=[size of result list]

### افزودن رویداد از طرف کسب و کار برای مشتری

در صورتی که کسب و کار نیاز داشته باشد، رویدادی برای کاربر خود اضافه نماید، مثلا جهت یادآوری به کاربر برای پرداخت فاکتور یا بلیط خریداری شده، میتواند از روش های زیر با مشخصات ذکر شده استفاده نماید :

**1- ثبت رویداد صریح**

به تقویم خود رویداد مورد نظر را اضافه نماید و مشتری را به عنوان شرکت کننده (attendee) در رویداد ثبت نماید، و اختیارات لازم را به مشتری جهت ویرایش رویداد، امکان دعوت سایرین و دیدن سایر شرکت کننده های رویداد را از این طریق به مشتری اعطا نماید.

با فراخوانی سرویس افزودن رویداد با پارامترهای دلخواه و ثبت کردن اطلاعات مشتری در قسمت شرکت کنندگان (attendees)، مشتری امکان دیدن این رویداد را خواهد داشت.

**2- ثبت رویداد ناشی از فاکتور**

در صورتی که کاربر در حال دریافت خدمات غیر رایگان باشد و کسب و کار نیاز به صدور فاکتور داشته باشد، کسب و کار میتواند هنگام صدور فاکتور رویداد مرتبط با آن همراه با لیست عملیات قابل اجرا توسط مشتری را ارسال نماید. بدین ترتیب یک رویداد شامل دکمه های عملیات مورد نظر، در تقویم کاربر قرار می گیرد.

### جستجوی رویدادها

نام این سرویس searchEvents  می باشد. جهت جستجوی رویداد یا رویدادهایی که کاربر دسترسی به دیدن آنها را دارد به کار میرود.
برای استفاده از این سرویس از نمونه کد زیر میتوانید کمک بگیرید: 

    HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
            PUT
    Url:
            [platform-address]/nzh/searchEvents/
    Parameters:
            _token_=[user token]
            _token_issuer_=1
            attendeeOrOwner=[identity of attendee or event Owner]
            titleOrDescription=[name of calendar or part of calendar description]
            longitude=[longitude]
            latitude=[latitude]

### بازیابی رویداد(ها)

#### بازیابی رویداد

جهت بازیابی رویداد بنا به شرایط مختلف سه سرویس در نظر گرفته شده است :

 **بازیابی رویداد با دادن شناسه آن**

    HEADER  _token_=[API_TOKEN] & _token_issuer_=1
    GET  [platform-address]/nzh/getEventById/
    ?eventId=[identifier of event]

 **بازیابی تمام رویدادهای مربوط به یک تقویم خاص**

    HEADER  _token_=[API_TOKEN] & _token_issuer_=1 GET  [platform-address]/nzh/getCalendarEvents/ ?calendarId=[identifier of calendar]

**سرویس جستجوی رویدادها**

    HEADER  _token_=[API_TOKEN] & _token_issuer_=1
    GET  [platform-address]/nzh/searchEvents/
    ?titleOrDescription=[title or description of event]

### حذف رویداد

نام این سرویس  deleteEvent میباشد و برای حذف رویداد شناسه رویداد به عنوان ورودی داده میشود و در صورت موفقیت آمیز بودن عملیات حذف پیغام مناسب فرستاده میشود.

برای حذف رویداد از دستور زیر استفاده نمایید:

    HEADER  _token_=[API_TOKEN] & _token_issuer_=1
    DELETE  [platform-address]/nzh/deleteEvent/
    ?eventId=[identifier of event]

### بازیابی مهمان رویداد با شناسه

برای بازیابی مهمان رویداد با شناسه از سرویس زیر استفاده نمایید:

    HEADER  _token_=[API_TOKEN] & _token_issuer_=1
    GET  [platform-address]/nzh/getAttendeeById/
    ?id=[identifier of event attendee]

### بازیابی فرد مشترک در تقویم با شناسه
برای بازیابی فرد مشترک در تقویم از سرویس زیر استفاده نمایید:

    HEADER  _token_=[API_TOKEN] & _token_issuer_=1
    GET  [platform-address]/nzh/getSharePersonById/
    ?id=[identifier of calendar share person]

###  بازیابی یادآور با شناسه

    HEADER:
            _token_=[API_TOKEN]
            _token_issuer_=1
    Method: GET
    Url:
            [platform-address]/nzh/getReminderById/
    Parameters:
            id=[identifier of event reminder]

### افزودن تقویم به علاقه مندی

در صورتی کاربر بخواهد تقویم خاصی که دسترسی عمومی یا نیمه عمومی دارد را به لیست تقویم های خود اضافه نماید (**subscribe**  ) از این سرویس استفاده میشود

ورودی این سرویس شناسه تقویم میباشد.

نام سرویس : **addCalendarToFavorites**

ورودی : **calendarId** - شناسه تقویم عمومی مورد نظر

    HEADER
    	_token_=[API_TOKEN]
    	_token_issuer_=1
    Method:
            GET
    Url:
            [platform-address]/nzh/addCalendarToFavorites/
    Parameters:
            calendarId=           //identifier of calendar

<div class="box-end">
</div>


##  اعلان 
این سرویس این امکان را در اختیار شما قرار می‌دهد که از طریق ایمیل، پیام کوتاه و اعلان اطلاع‌رسانی‌های لازم را در اختیار کاربران و گردشگران قرار دهید.

### نصب -نسخه اندروید

پکیج اندرویدی نوتیفیکیشن را میتوانید از لینک زیر و با استفاده از گیت دریافت کنید یا فایل زیپ آن را دانلود نمایید.
[لینک گیت‌هاب](https://github.com/smartPodLand/Pod-Notification-Android-SDK)


**راهنمای نصب با استفاده از اندروید استودیو:**

+  پروژه خود را با استفاده از AndroidStudio باز کنید و با استفاده از منوی File زیر منوی Import Module پکیج اندرویدی نوتیفیکیشن را به پروژه خود اضافه کنید.
+  در پروژه ی خود بر روی ماژول app راست کلیک کرده و گزینه ی "Open Module Settings" را انتخاب کنید.
+ بر روی تب Dependencies کلیک کرده و گزینه ی + را کلیک کنید.
+ پس از انتخاب  Module Dependency میتوانید ماژول نوتیفیکیشن را به پروژه اضافه کنید.


**پیش‌نیازها:**پیش از هر چیز در کلاس application برنامه خود، با استفاده از متد زیر، context برنامه را اضافه کنید:


```
PodNotify.setApplication(this);
```


در اولین قدم می‌توانید با استفاده از نمونه کد زیر شی نمونه از ماژول را بسازید:


```

PodNotify podNotify = new PodNotify.builder()
                            .setAppId("APP_ID")
                            .setServerName("SERVER_NAME")
                            .setSocketServerAddress("SERVER_SOCKET_ADDRESS")
                            .setSsoHost("SSO_HOST_IF_NEEDED")
                            .setToken("TOKEN")
                            .setDeviceId("STABLE_DEVICE_ID")
                            .build();
```


پس از آن می‌توانید مشابه نمونه زیر، سرویس را استارت کنید:


```

podNotify.start(getApplicationContext());
```




###  دریافت و نمایش اعلان

مانند نمونه کد زیر، برای دریافت و نمایش اعلان‌ها و همچنین استفاده از extras data باید پس از ساخت یک service، آن را از کلاس PodMessagingService ارث بری کنید:


```

public class MyMessagingService extends PodMessagingService {

    @Override
    public void onMessageReceived(Notification notification) {
        //your code that use Notification object
        super.onMessageReceived(notification);
    }
}
```




توجه کنید که برای نمایش اعلان دریافت شده حتما میبایست مقدار super.onMessageReceived(notification); را استفاده کنید و درصورت حذف آن، فقط اطلاعات اعلان دریافت شده در دسترس است و می‌توانید از آن استفاده کنید.

اطلاعات ارسال شده به عنوان اعلان از جنس شی Notification بوده و میتوان از طریق متدهای getter و setter به آن دسترسی داشت.


```

public class Notification {

    private String title;
    private String text;
    private Long messageId;
    private String senderId;
    private Map<String,String> extras;
    
    // Getters and setters for fields.
}
```




ضمنا در نظر داشته باشید که برای دریافت صحیح اعلان باید سرویس گفته شده در مرحله قبل، در Android Manifest حتما به شکل زیر تعریف شده باشد.



```


<service
  android:name=".MyMessagingService">
      <intent-filter>
          <action android:name="com.fanap.podnotify.MESSAGING_EVENT"/>
      </intent-filter>
</service>
```



نکته: به هیچ‌وجه action استفاده شده در تعریف بالا را حذف نکنید یا تغییر ندهید.



###  دریافت PeerId

برای دریافت peerId جدید و ارسال و یا ذخیره آن می‌توان مانند با ساخت یک service، و ارث بری از PodInstanceIdService عمل کرد:


```

public class MyInstanceIdService extends PodInstanceIdService {

    @Override
    public void onPeerIdChanged(String peerId) {
        //your code... (eg. send PeerId to your server)
        super.onPeerIdChanged(peerId);
    }
}
```



اطلاعات ارسال شده از جنس رشته string بوده و می‌توان در هر تغییر به آن دسترسی داشت.

سرویس ساخته شده باید برای کارکرد درست در Android Manifest به صورت زیر تعریف شود:

```

<service
  android:name=".MyInstanceIdService">
      <intent-filter>
          <action android:name="com.fanap.podnotify.INSTANCE_ID_EVENT"/>
      </intent-filter>
</service>
```



حتما توجه کنید که در action منتسب به سرویس به هیچ‌وجه تغییری ایجاد نشود.

<div class="box-end">
</div>

### نصب-نسخه جاوا اسکریپت

در صورتی که npm یا yarn را نصب دارید، میتوانید با خط دستور زیر سرویس نوتیفیکیشن را بر روی پروژه ی خود نصب نمایید. 

دستور نصب با npm

    npm install pod-notify-js


دستور نصب با yarn

    yarn add pod-notify-js


یا از طریق لینک زیر اقدام به دریافت فایل زیپ پروژه نمایید و آن را در محل پروژه ی خود extract کنید:


لینک گیت هاب
[لینک npm](https://www.npmjs.com/package/pod-notify-js)




**ساخت نمونه اولیه:**

اولین قدم ساخت یک شیء نمونه از ماژول PodNotify است.

    var PodNotify = require('./src/chat.js');
    // ES6: import PodNotify from 'pod-notify-js';
    
    //params doc => https://docs.pod.land/document/notification-javascript-config
    var params = {
        socketAddress: "ws://server.address/ws", // {**REQUIRED**} Socket Address
        serverName: 'your_server_name', // {**REQUIRED**} Server Name
        token: 'your_app_token_here', // {**REQUIRED**} Your App Token Here
        handlePushNotification: true //If you want notification to be handle by podnotify
    };
    
    var podNotify = new PodNotify(params)



آدرس ها و تنظیمات لازم را به صورت لیستی از پارامترها به عنوان params به ورودی نمونه خود بدهید، توجه داشته باشید پروژه دارای فایل index.d.ts هست در نتیجه در صورت استفاده از editor های دارای پشتیبانی Typescript دارای Intellisense خواهید بود. 



### تنظیمات اولیه

برای دریافت یا تنظیم تنظیمات کافیست متغیر config را گرفته و تغییر ایجاد کنید:

    podNotify.config = {};
    console.log(podNotify.config); // {}




### دریافت و نمایش اعلان

برای نمایش اعلان میتوانید با قرار دادن _handlePushNotification: true_ به عنوان param اجازه دهید تا توسط PodNotify اعلان نمایش داده شود یا به صورت سفارشی سازی پس از دریافت اعلان نمایش دهید.

برای دریافت اعلان نیز کافیست تا Event Listener ی تعریف کنید با نام message و اطلاعات را دریافت کنید:


    var podNotify = new PodNotify(params)
    podNotify.on(“message”, function(response) {
        console.log(response);
     /* {
            title: string;
            text: string;
            messageId: number;
            senderId: number;
            extras: any[];
        } */
    });



_نکته: جهت حذف این listener  میتوانید از متد off استفاده کنید_


    var podNotify = new PodNotify(params)
    var id = podNotify.on(“message”, function(response) { });
    podNotify.off(“message”, id);// returns Boolean, true if successfully removed



### ,Event Listeners


**متد on:**

این متد در پارامتر اول رشته نام رویداد (event) را دریافت می کند و در پارامتر دوم متد callback را دریافت میکند و یک id ساخته شده برمیگرداند که در صورت لزوم میتوان برای حذف کردن این event از این id استفاده کرد.

_مثال:_


    var id = podNotify.on(“message”, function(response) { }); // :string


**متد off:**

از این متد میتوان در جهت حذف کردن رویداد (event) ساخته شده استفاده کرد. این متد در پارامتر اول نام event را دریافت میکند و در پارامتر دوم id ساخته شده در زمان فراخوانی متد on را دریافت میکند.

_مثال:_


    podNotify.off(“message”, id);// returns Boolean, true if successfully removed




### سفارشی سازی

    var notifyInstance = podNotify.notify; // returns notify class
    notifyInstance.Permission; // returns PushPermission class
    notifyInstance.create(‘title’, {}); // create and show notification




### دریافت مشخصات یکتای دستگاه

برای دریافت مشخصات یکتای دستگاه کافیست متغیر clientUniques را دریافت کنید:

    console.log(podNotify.clientUniques); // ClientUniques
    podNotify.clientUniques.browser; // “Chrome”
    podNotify.clientUniques. browserMajorVersion; // “56”

<div class="box-end">
</div>


## پیام رسان 
با استفاده از این سرویس می‌توانید با گردشگرانی که از خدمات شما استفاده می‌کنند در ارتباط باشید و به سوالات و مشکلات احتمالی آن‌ها در اسرع وقت رسیدگی کنید.

### نصب- جاوا اسکریپت

در صورتی که npm را نصب دارید، میتوانید با خط دستور زیر سرویس پیام رسان را بر روی پروژه ی خود نصب نمایید.

    npm install podchat --save

یا از طریق لینک زیر اقدام به دریافت فایل زیپ پروژه نمایید و آن را در محل پروژه ی خود extract کنید:

لینک گیت‌هاب:
https://github.com/FanapSoft/podchat

لینک npm:
https://www.npmjs.com/package/podchat


**یشپنیازها**

هر کاربر جهت ورود نیازمند به یک توکن دسترسی است.

توکن دسترسی باید قبل از استفاده از سرویس پیام رسان ، از سرور sso دریافت شود تا به هنگام ساخت نمونه ی اولیه از شیء این سرویس به عنوان پارامتر به آن داده شود.


**ساخت نمونه اولیه:**

اولین قدم ساخت یک شیء نمونه از ماژول چت است.


    var ChatSdk = require('podchat');
    
    //params doc => https://docs.pod.land/document/chat-javascript-config
    var Chat = new ChatSdk(params),



آدرس ها و تنظیمات لازم را به صورت لیستی از پارامترها به عنوان params به ورودی نمونه خود بدهید.


### مدیریت مخاطبین

**۱- getContacts:**

دریافت لیست مخاطبین. این متد یک لیست جهت تنظیمات صفحه‌بندی (حداکثر تعداد مخاطبین در هر درخواست و شماره ی  شروع) دریافت می کند و لیست تمامی مخاطبین کاربر را بازمی‌گرداند.

به عنوان ورودی دوم نیز یک callback function دریافت می کند که پس از دریافت جواب اجرا خواهد شد.


    var Params = {
       count: 50, //{**OPTIONAL**}
       offset: 0  //{**OPTIONAL**}
    };
    
    Chat.getContacts(Params, function(contactsResult) {
        console.log(contactsResult);
      });



**۲- addContacts:**

جهت اضافه کردن یک مخاطب جدید از این متد استفاده کنید. باید لیستی از مشخصات کاربر جدید را به عنوان ورودی در این تابع قرار دهید.نتیجه ی عملیات در callback قابل دریافت است.

_نکته:_

_در صورت ارسال مقدار پارامترfirstName برای مخاطب، اجباری به ورود پارامتر نام خانوادگی(و بالعکس) نمی باشد و هم چنین در صورت ورود شماره موبایل، ورود ایمیل الزامی نیست(و بالعکس)._

_اما توجه داشته باشید ارسال مقادیر پارامتر(اگرچه بدون مقدار ورودی) الزامی می باشد_


     Chat.addContacts({
        firstName: "Sina",
        lastName: "Rahimi",
        cellphoneNumber: "0912*****85",
        email: "sinarahimi1@gmail.com"
      }, function(result) {
        console.log(result);
      });


**۳- updateContact:**

مشخصات جدید کاربر را به همرا id (همان آیدی مخاطب که پس از ذخیره ، یا به هنگام استفاده از سرویس لیست مخاطبین دریافت کرده اید) در لیست پارامتر ورودی به این متد بدهید تا عملیات تغییر مشخصات مخاطب مورد نظر صورت گیرد. پاسخ مشابه سرویس قبلی خواهد بود.
  

    Chat.updateContacts({
        id: "661",
        firstName: "mohammad javad",
        lastName: "Rahimi",
        cellphoneNumber: "0938*****55",
        email: "newMail@gmail.com"
      }, function(result) {
        console.log(result);
      });


**۴- removeContact:** 

با دریافت آیدی مخاطب، مشخصات آن را حذف میکند.

  

    Chat.removeContacts({
        id: "661" //{**REQUIRED**}
      }, function(result) {
        console.log(result);
      });


**۵-blockContact:**

با دریافت آیدی مخاطب،امکان ارتباط با او را مسدود میکند.


  

    var data = {
        contactId: contactId //Required
      }
    
      Chat.block(data, function(result) {
        console.log(result);
      });




**۶- getBlockList:**

لیست مخاطبین بلاک شده را بازمیگرداند.

با پر کردن مقادیر ورودی count و offset میتوانید تنظیمات صفحه بندی را اعمال کنید.



 

     var data = {
        count: 50,
        offset: 0
      }
    
      Chat.getBlocked(data, function(result) {
         console.log(result);
      });



**۷-unblock:**

با دریافت blockId (آیدی مخاطب از لیست مسدود شده ها)، امکان ارتباط مجدد با مخاطب را برقرار میکند و مخاطب از لیست مسدود شده ها خارج میشود.

  

    var data = {
        blockId: blockId //Required
      }
      Chat.unblock(data, function(result) {
        console.log(result);
      });});



**۸- searchContact:**

با دریافت پارامترهای زیر، از بین مخاطبین کاربر به جستجو پرداخته و لیستی از مخاطبین با مشخصات داده شده را بازمیگرداند.



    /*
    *cellphoneNumber
    *email
    *firstName
    *lastName
    *uniqueId
    *id
    *offset 
    *size 
    *typeCode
    *q
    */
    
      Chat.searchContacts({
        cellphoneNumber: 099
      }, function(result){
        if (!result.hasError) {
          console.log(result);
        }
      });


### مدیریت پیام ها

**۱- sendTextMessage:**

ارسال پیام به یک ترد، با دریافت آیدی ترد و پیغام ارسالی. این متد لیستی شامل سه callback function دریافت میکند که برای مدیریت کاربر پس از ارسال پیغام(send) ، دریافت (deliver) و دیده شدن پیغام ارسالی توسط دیگر اعظای ترد(seen) است.

 

     sendChatParams = {
        threadId: threadId,  //{**REQUIRED**}
        content: message  //{**REQUIRED**}
      };
    
      Chat.send(sendChatParams, {
        onSent: function(result) {
           //your_code_for_sent_msg_in_app
          //console.log("\nYour message has been Sent!\n"); 
          console.log(result);
        },
        onDeliver: function(result) {
          //your_code_for_delivered_msg_in_app
          //console.log("\nYour message has been Delivered!\n"); 
          console.log(result);
        },
        onSeen: function(result) {
          //your_code_for_seen_msg_in_app
          //console.log("\nYour message has been Seen!\n"); 
          console.log(result);
        }
      });



_**نکته:**_ 

+ _سرویس پیام رسان (ارسال کننده ی پیغام)، تحویل پیغام به گیرنده را (از طریق متد deliver) به کاربر(فرستنده ی پیغام)اعلام میکند.__(_[Event Listeners](https://docs.pod.land/document/chat-javascript-eventlisteners)_)_
+ _کاربر دریافت کننده ی پیغام باید رویت پیغام را از طریق متد seen به سرور(فرستنده ی پیغام) اعلام کند._


**_۲- editMessage:_**

_با دریافت آیدی پیام و محتوای جدید ، پیغام مربوطه را ویرایش میکند._

_نکته: سرور نتیجه ی تغییر پیغام را بر روی رویداد "_messageEvents_" با نوع "_MESSAGE_EDIT_" گزارش خواهد داد._ _(_[Event Listeners](https://docs.pod.land/document/chat-javascript-eventlisteners)_)_


  

    editChatParams = {
        messageId: messageId,  //{**REQUIRED**}
        content: newMessage  //{**REQUIRED**}
      };
    
      Chat.editMessage(editChatParams, function(result) {
        console.log(result);
      });




**۳- replyMessage:**

با دریافت آیدی ترد ، آیدی پیام ، و محتوای دلخواه ، پیام مورد نظر شما را انتخاب و محتوا را در پاسخ به آن پیام ارسال میکند.

با توجه به اینکه جنس این متد همانند sendTextMessage از نوع ارسال پیام است ، در نتیجه سه callback جهت عملیات پس از ارسال، دریافت، و دیده شدن پیام لازم خواهد داشت.


  

    replyChatParams = {
        threadId: threadId, //{**REQUIRED**}
        repliedTo: messageId, //{**REQUIRED**}
        content: message //{**REQUIRED**}
      };
    
      Chat.replyMessage(replyChatParams, {
        onSent: function(result) {
          //console.log(result.uniqueId + " \t has been Sent! (Reply)");
           console.log(result);
        },
        onDeliver: function(result) {
          //console.log(result.uniqueId + " \t has been Delivered! (Reply)"); 
        },
        onSeen: function(result) {
          //console.log(result.uniqueId + " \t has been Seen! (Reply)"); 
        }
      });



**۴- forwardMessage:**

این متد ، باز ارسال یک پیام انتخابی را به یک ترد مشخص، با استفاده از آیدی پیام (جهت انتخاب آن) و آیدی ترد مقصد انجام خواهد داد. نوع این متد نیز ارسال پیام است.


  

    Chat.forwardMessage({
        subjectId: destination, //threadId {**REQUIRED**}
        content: JSON.stringify(messageIds)  //{**REQUIRED**}
      }, {
        onSent: function(result) {
          //console.log(result.uniqueId + " \t has been Sent! (FORWARD)");
          console.log(result);
        },
        onDeliver: function(result) {
          console.log(result.uniqueId + " \t has been Delivered! (FORWARD)");
        },
        onSeen: function(result) {
          console.log(result.uniqueId + " \t has been Seen! (FORWARD)");
        }
      });


_نکته: متد باز ارسال میتواند لیستی از پیام ها را با دریافت آیدی پیام ها به ترد مقصد ارسال کند. در این حالت برای هر پیام یک uniqueId جداگانه خواهد بود._

_مثال:_

    destination = 312;
    messageIds = [2539, 2538, 2537];
    Chat.forwardMessage({
        subjectId: destination, //threadId
        content: JSON.stringify(messageIds)
      }, {
        onSent: function(result) {
          //console.log(result.uniqueId + " \t has been Sent! (FORWARD)");
          console.log(result);
        },
        onDeliver: function(result) {
          console.log(result.uniqueId + " \t has been Delivered! (FORWARD)");
        },
        onSeen: function(result) {
          console.log(result.uniqueId + " \t has been Seen! (FORWARD)");
        }
      });



**۵- sendFileMessage:**

ارسال پیام با محتوای فایل به یک ترد مشخص. با دریافت آیدی ترد مقصد، آدرس فایل مورد نظر، محتوای متن همراه عکس و محتوای مورد نظر متادیتا، فایل ارسالی را پس از آپلود بر روی سرور، به همراه پیام ارسالی به ترد مقصد ارسال میکند.


    Chat.sendFileMessage({
        threadId: threadId, //{**REQUIRED**}
        file: file, //{**REQUIRED**}
        content: caption,
        metaData: metaData
      }, {
        onSent: function(result) {
          console.log(result.uniqueId + " \t has been Sent!");
        },
        onDeliver: function(result) {
          console.log(result.uniqueId + " \t has been Delivered!");
        },
        onSeen: function(result) {
          console.log(result.uniqueId + " \t has been Seen!");
        }
      });



_نکته مهم: در صورتی که از فرم html استفاده میکنید به صورت مثال زیر آپلود نمایید._



    /* html */
    
    <form>
      <fieldset>
        <legend>Send File Message</legend>
        <input type="file" name="sendFileInput" id="sendFileInput">
        <br>
        <label for="sendFileDescription">Description: </label>
        <input type="text" name="sendFileDescription" id="sendFileDescription">
        <button type="button" name="button" id="sendFileMessage">Send</button>
      </fieldset>
    </form>




    /* js */
    
    document.getElementById("sendFileMessage").addEventListener("click", function() {
      var fileInput = document.getElementById("sendFileInput"),
        image = fileInput.files[0],
        content = document.getElementById("sendFileDescription").value;
    
      Chat.sendFileMessage({
        threadId: 293,
        file: image,
        content: content,
        metaData: {custom_name: "John Doe"}
      }, {
        onSent: function(result) {
         // console.log(result.uniqueId + " \t has been Sent!");
        },
        onDeliver: function(result) {
         // console.log(result.uniqueId + " \t has been Delivered!");
        },
        onSeen: function(result) {
         // console.log(result.uniqueId + " \t has been Seen!");
        }
      });
    });


**۶- deleteMessage:**

با دریافت آیدی پیام (messageId) ، پیام مربوطه را حذف خواهد کرد.

نکته: در صورتی که متغیر deleteForAll را با مقدار true پر کنید ، پیام مذکور از تاریخچه ی ترد همه ی اعضای آن ترد پاک خواهد شد.

  

    Chat.deleteMessage({
        messageId: messageId, //{**REQUIRED**}
        deleteForAll: deleteForAll 
      }, function(result) {
        console.log(result);
      });





_نکته: کلاینت های دیگر عضو این ترد، پس از پاک شدن یک پیغام از طریق رویدادهای ترد، با نوع THREAD_INFO_UPDATED مطلع میشوند_


**7- deleteMultipleMessages:**

با دریافت آیدی ترد (threadId) و لیستی از آیدی پیام ها (messageIds) پیام های مربوطه را حذف خواهد کرد.

نکته: در صورتی که متغیر deleteForAll را با مقدار true پر کنید ، پیام مذکور از تاریخچه ی ترد همه ی اعضای آن ترد پاک خواهد شد.



    chatAgent.deleteMultipleMessages({
        threadId: 10298,
        messageIds: [47710, 47709, 47708],
        deleteForAll: true
    }, function(result) {
        console.log("Delete Multiple Message Result", result);
    });





بعد از ارسال دستور بالا، به ازای هر کدام از پیام های موجود در لیست آرایه ایه messageIds، یکبار Callback تعیین شده اجرا میشود. همچنین یک event مربوط به حذف پیام نیز توسط سرور ارسال میگردد.

    // Callback
    
    {
      hasError: false,
      cache: false,
      errorMessage: '',
      errorCode: 0,
      result: { deletedMessage: { id: 49228 } } 
    }
    
    // Message Delete Event
    
    { 
      type: 'MESSAGE_DELETE',
      result: { message: { id: 49228, threadId: 10424 } } 
    }


### مکانیزم Seen برای پیام ها

جهت اینکه برای پیام های ارسالی در یک ترد، به فرستنده،  پیام Seen ارسال شود. لازم است کلاینت از تابع chatAgent.seen() استفاده نماید.

چنانچه کلاینت آنلاین بوده و در داخل یک ترد در حال گفتگو باشد میتواند به محض مشاهده ی پیام برای پیام دیده شده Seen ارسال کند. اما اگرتعدادی پیام در یک ترد ارسال شده و کاربر بعد از مدتی وارد ترد شود، بایستی برای آخرین پیام دریافتی Seen ارسال کند. 

_**\* تبصره:**_ برای جلوگیری از ارسال Seen تکراری برای آخرین مسیج ترد، کلاینت میتواند از مقادیر lastSeenMessageId و lastSeenMessageTime و مقایسه این مقادیر با ID یا Time مسیجی که میخواهد برای آن Seen بفرستد، از ارسال Seen اضافی جلوگیری نماید.

**\** سناریوهای Seen شدن اتوماتیک برای پیام ها در سرور**

- زمانی که کاربر برای یک پیام، Seen ارسال میکند، سرور چت بصورت اتوماتیک، مقدار seen تمامی پیام های قبل از این پیام را True ست میکند. لذا کلاینت نیز باید بعد از ارسال Seen برای یک مسیج، تغییرات مد نظر خود برای نمایش Seen خوردن مسیج را برای تمامی مسیج های قبلی نیز اعمال نماید.

- چنانچه کاربر در یک ترد مسیجی ارسال کند، مقدار Seen برای تمامی مسیج های دریافتی اش در سرور به True تغییر میکند. لذا همانند حالت قبل، کلاینت باید UI خود را با این فرض بروزرسانی کند.


###  مدیریت Cache

ساختار کش برای SDK بصورت کاملا داخلی پیاده سازی شده و نیازی به پیاده سازی دوباره ی کش برای چت نیست. مقادیر کش تماما با استفاده از کلیدهای دریافت شده برای کاربر از سمت سرور SSO رمزنگاری شده اند و امکان سو استفاده از مقادیر کش شده بر روی سیستم وجود ندارد. چنانچه کاربری سعی بر دسترسی به مقادیر کش شده با کلید نادرست نماید، تمامی مقادیر برای حفظ امنیت کاربر از روی کش پاک میشوند.  کش با استفاده از IndexedDb پیاده سازی شده و ساختار جداول به صورت زیر میباشد:


    users: '&id, name, cellphoneNumber, keyId',
    contacts: '[owner+id], id, owner, uniqueId, userId, cellphoneNumber, email, firstName, lastName, expireTime',
    threads: '[owner+id] ,id, owner, title, time, [owner+time]',
    participants: '[owner+id], id, owner, threadId, notSeenDuration, admin, name, contactName, email, expireTime',
    messages: '[owner+id], id, owner, threadId, time, [threadId+id], [threadId+owner+time]',
    messageGaps: '[owner+id], [owner+waitsFor], id, waitsFor, owner, threadId, time, [threadId+owner+time]'


_**نکته:**_ جهت بهره برداری از سیستم کش، بایستی مقدار پارامتر enableCache در پارامترهای اولیه ی ورودی SDK چت به صورت True ست نمائید.


1- **,clearCacheDatabasesOfUser** :

سیستم کش پادچت بصورت چندین کاربره طراحی شده و چنانچه چندین کاربر با یک سیستم از چت استفاده نمایند، اطلاعات هرکدام با استفاده از کلیدهای رمزنگاری خود آن کاربر بر روی دیتابیس های کش ذخیره میشود. 

چنانچه بخواهید اطلاعات کش شده ی مربوط به کاربر جاری را از کش پاک کنید، کافیست متد clearCacheDatabasesOfUser را فراخوانی نمائید.


    chatAgent.clearCacheDatabasesOfUser();




2- **,deleteCacheDatabases** :

چنانچه بخواهید اطلاعات کش شده ی مربوط به تمامی کاربران را از کش پاک کنید، کافیست متد **deleteCacheDatabases** را فراخوانی نمائید. این متد تمامی جداول کش را حذف نموده و دوباره میسازد.



    chatAgent.deleteCacheDatabases();



### مدیریت فایل‌ها  

سرویس های مدیریت فایل شامل موارد زیر میشود:

**۱- uploadImage:** 

با دریافت آدرس فایل عکس ، آن را بر روی سرور فایل ذخیره میکند. در صورتی که میخواهید عکس را برش دهید ، مختصات شروع برش و طول و عرض برش را به عنوان ورودی به متد ارسال کنید.

برش عکس


      Chat.uploadImage({
        image: "/your/image/path",
        xC: xC,
        yC: yC,
        hC: hC,
        wC: wC
      }, function(result) {
          console.log(result);
      });


_نکته مهم: در صورتی که از فرم html استفاده میکنید به صورت مثال زیر آپلود نمایید._


    /* html */
    
    <form>
      <fieldset>
        <legend>Upload Image</legend>
        <input type="file" name="image" id="imageInput" value="">
        <button type="button" name="button" id="uploadImage">Upload Image</button>
        <br>
        <img id="uploadedImage" />
        <div id="uploadedImageData"></div>
      </fieldset>
    </form>



    /* js */
    
    document.getElementById("uploadImage").addEventListener("click", function() {
      var imageInput = document.getElementById("imageInput"),
        image = imageInput.files[0];
    
      Chat.uploadImage({
        image: image,
        fileName: "Test Name",
        xC: 0,
        yC: 0,
        hC: 800,
        wC: 800
      }, function(result) {
        if (!result.hasError) {
          //your_code
        }
      });
    });



**۲- getImage:**

با دریافت آیدی تصویر ذخیره شده و کد مشخصه ی آن (hashCode) لینک دریافت آن را در اختیار قرار میدهد.


     Chat.getImage({
        imageId: imageId,
        hashCode: hashCode
      }, function(result) {
        if (!result.hasError) {
          console.log(result);
        }
      });



**۳- uploadFile:**

با دریافت آدرس فایل آن را در سرور فایل بارگذاری خواهد کرد.

    Chat.uploadFile({
        file: file
      }, function(result) {
          console.log(result);
      });




_نکته مهم: در صورتی که از فرم html استفاده میکنید به صورت مثال زیر آپلود نمایید._

    /* html */
    
    <form>
      <fieldset>
        <legend>Upload File</legend>
        <input type="file" name="file" id="fileInput" value="">
        <button type="button" name="button" id="uploadFile">Upload File</button>
        <br>
        <div id="uploadedFile"></div>
      </fieldset>
    </form>



    /* js */
    
    document.getElementById("uploadFile").addEventListener("click", function() {
      var fileInput = document.getElementById("fileInput"),
        file = fileInput.files[0];
    
      Chat.uploadFile({
        file: file,
        fileName: "Test Name"
      }, function(result) {
        if (!result.hasError) {
          //your_code
        }
      });
    });




**۴- getFile:**

با دریافت آیدی فایل ذخیره شده و کد مشخصه ی آن (hashCode) لینک آن را در اختیار قرار میدهد.این متد پارامتری به عنوان downloadable دارد که از نوع boolean است. در صورت مثبت بودن لینک فایل خروجی قابل دانلود خواهد بود.


      Chat.getFile({
        fileId: fileId,
        hashCode: hashCode,
        downloadable: downloadable
      }, function(result) {
        if (!result.hasError) {
          //your_code
        }
      });


## مدیریت پروفایل

**۱- getUserInfo:**

این متد اطلاعات پروفایل کاربر را در اختیارش قرار میدهد. با توجه به توکن دسترسی عمل میکند، لذا نیازی به ورودی ندارد.

 

     Chat.getUserInfo(function(userInfo) {
        console.log(userInfo);
      });



**2 - isTyping:**

این متد دارای دو بخش متفاوت میباشد. در کل هدف ارسال بسته هایی شامل اطلاعات فرد در حال تایپ به سرور میباشد که سرور بتواند طرفین مقابل را از وضعیت تایپ کردن یوزر مطلع سازد.

برای استفاده از این امکان، کافیست همزمان با شروع تایپ توسط کاربر متد startTyping فراخوانی شده و مقدار threadId بدان ارسال شود. به صورت زیر: 


    chatAgent.startTyping({threadId: 1431});

با فراخوانی متد startTyping به صورت اتوماتیک هر 1 ثانیه یکبار پیامی حاوی اطلاعات لازم برای سرور ارسال میگردد. در صورتی که عملیات تایپ کردن توسط کاربر به اتمام رسید. میتوانید با فراخوانی متد stopTyping طرفین مقابل و سرور را از این موضوع باخبر سازید. به صورت زیر:


    chatAgent.stopTyping();




### Event Listeners 


**متد on:**

رخداد تمامی رویداد ها با متد on قابل دریافت خواهد بود. رویداد های قابل مشاهده شامل موارد زیر است:


**۱- messageEvents:**

تمامی رویدادهایی که پس از فعل و انفعال پیام ها قابل رخداد است با این نام قابل دریافت است. message events یا رویدادهای پیام دلایل مختلفی دارد ، که به فراخور آن میتوانید عملیات مورد نظر خود را سمت اپلیکیشن انجام دهید.


    /**
     \* Listen to Message Events
     \*/
    Chat.on("messageEvents", function(event) {
      var type = event.type,
        message = event.result.message;
    
      console.log(event);
    
      switch (type) {
        case "MESSAGE_NEW":
          /**
           \* Sending Message Seen to Sender after 5 secs
           \*/
          setTimeout(function() {
            Chat.seen({messageId: message.id, ownerId: message.ownerId});
          }, 5000);
    
          break;
    
        case "MESSAGE_EDIT":
          //your_code
          break;
    
        case "MESSAGE_DELIVERY":
          break;
    
        case "MESSAGE_SEEN":
          break;
    
        default:
          break;
      }
    });



,message events شامل event های زیر است:

, MESSAGE_NEW: با دریافت پیام جدید این رویداد رخ خواهد داد.
 ,MESSAGE_EDIT: ویرایش شدن یک پیغام در ترد، از طریق این رویداد به اعضای آن ترد اطلاع داده میشود.
 ,MESSAGE_DELIVERY: دریافت پیام توسط گیرنده توسط این رویداد به فرستنده اطلاع رسانی میشود.
 ,MESSAGE_SEEN: پس از دیده شدن پیغام توسط کاربر گیرنده ی پیام ، فرستنده توسط این رویداد از این امر مطلع میشود.



**۲- threadEvents:**

تمامی رویداد های ترد هایی که کاربر در آن عضو است یا به آن مرتبط میباشد از این طریق اعلام میشود. رویدادهای مربوط به ترد ، انواع زیر را داراست که بسته به نوع آن میتوانید عملیات متناسب را سمت اپلیکیشن خود انجام دهید.

, THREAD_NEW: ساخت ترد جدید را به اعضایی که در آن مشارکت خواهند داشت (Participants) اعلام میکند.
 ,THREAD_LAST_ACTIVITY_TIME: زمانی که فعل و انفعالی در یک ترد رخ دهد، زمان آخرین فعل و انفعال رخ داده به اعضای آن ترد اعلام خواهد شد.(اپلیکیشن جهت آپدیت لیست تردها بر اساس جدیدترین تغییرات آنها میتواند اقدام کند)
 ,THREAD_ADD_PARTICIPANTS: اضافه شدن فرد جدید به یک ترد را به همه ی اعضا اعلام میکند.
 ,THREAD_LEAVE_PARTICIPANTS: ترک کردن ترد توسط یک فرد را به اعضا اعلام میکند.
 ,THREAD_REMOVE_PARTICIPANTS: حذف شدن یک فرد از ترد را به اعضا اعلام میکند.
, THREAD_REMOVED_FROM: حذف شدن یک فرد از ترد را به او اعلام میکند.
 ,THREAD_RENAME: تغییر نام ترد توسط این رویداد به هر یک از اعضا اعلام میشود.
 ,THREAD_MUTE: پس از غیرفعال کردن نوتیفیکیشن یک ترد توسط کاربر به او اعلام میشود.
 ,THREAD_UNMUTE: پس از فعال کردن نوتیفیکیشن یک ترد توسط کاربر به او اعلام میشود.
, THREAD_INFO_UPDATED: در صورتی که اطلاعات داخل ترد نیاز به به روز رسانی داشته باشد (مثل زمانی که یک پیغام پاک میشود)، توسط این رویداد به دیگر اعضا اطلاع رسانی میشود.
 ,THREAD_UNREAD_COUNT_UPDATED: تعداد پیغام های خوانده نشده ی هر ترد توسط این رویداد به اعضای آن اعلام میشود.اپلیکیشن میتواند در لیست ترد های نمایش داده به کاربر ، تعداد پیغام های خوانده نشده ی هر کدام را اعلام کند.در صورتی که پیغام جدیدی به هر تردی اضافه شود ، تعداد پیغام های خوانده نشده ی آن آپدیت و بدین وسیله به کاربر (اعضای آن ترد) گزارش میشود.



    /**
     * Listen to Thread Events
     */
    Chat.on("threadEvents", function(event) {
      var type = event.type;
    
      switch (type) {
        case "THREAD_LAST_ACTIVITY_TIME":
          //your_code_here
          break;
    
        case "THREAD_NEW":
          //your_code_here
          break;
    
        case "THREAD_ADD_PARTICIPANTS":
          //your_code_here
          break;
    
        case "THREAD_REMOVE_PARTICIPANTS":
          //your_code_here
          break;
    
        case "THREAD_LEAVE_PARTICIPANT":
          //your_code_here
          break;
    
        case "THREAD_REMOVED_FROM":
          //your_code_here
          break;
    
        case "THREAD_RENAME":
          //your_code_here
          break;
    
        case "THREAD_MUTE":
          //your_code_here
          break;
    
        case "THREAD_UNMUTE":
          //your_code_here
          break;
    
        case "THREAD_INFO_UPDATED":
          //your_code_here
          break;
    
        case "THREAD_UNREAD_COUNT_UPDATED":
          //your_code_here
          break;
    
        default:
          break;
      }
    });



**۳- error:**

تمامی خطا ها از سمت سرور توسط این رویداد به کاربر گزارش میشود.

    /**
    * Listen to Error Messages
    */
    Chat.on("error", function(error) {
      console.log("ERROR \t", error.code, error.message, error.error);
    });



**۴- chatState:**

تغییر وضعیت ارتباط با سرور پیام رسان را به کاربر اطلاع میدهد.

چهار وضعیت CONNECTED,CONNECTING,CLOSED,CLOSING قابل رخداد است.

    /**
    \* Listen to Chat State Changes
    \*/
    chatAgent.on("chatState", function(chatState) {
    // your_code
    });






### آدرس ها و تنظیمات

تنظیمات و آدرس های زیر (برای سرور سندباکس) ، باید به عنوان پارامتر ورودی در هنگام ساخت نمونه ی اولیه از پکیج داده شود.



    var params = {
        appId: new Date().getTime(),
        socketAddress: 'ws://172.16.110.131:8003/ws', // {**REQUIRED**} Socket Address
        ssoHost: 'http://172.16.110.76', // {**REQUIRED**} Socket Address
        platformHost: 'http://172.16.110.131:8080', // {**REQUIRED**} Platform Core Address
        fileServer: 'http://172.16.110.131:8080', // {**REQUIRED**} File Server Address
        serverName: 'chat-server2', // {**REQUIRED**} Server to to register on
        grantDeviceIdFromSSO: false,
        enableCache: false, // Enable Client side caching
        fullResponseObject: true,
        mapApiKey: 'NESHAN_MAP_API_KEY',
        typeCode: "default",
        token: '7cba09ff83554fc98726430c30afcfc6', // {**REQUIRED**} SSO Token 
        wsConnectionWaitTime: 500, // Time out to wait for socket to get ready after open
        connectionRetryInterval: 5000, // Time interval to retry registering device or registering server
        connectionCheckTimeout: 10000, // Socket connection live time on server
        messageTtl: 24 * 60 * 60, // Message time to live (1 day in seonds)
        reconnectOnClose: true, // auto connect to socket after socket close
        asyncLogging: {
            onFunction: true, // log main actions on console
            onMessageReceive: true, // log received messages on console
            onMessageSend: true, // log sent messaged on console
            actualTiming: true // log actual functions running time
        }
    }


## نصب- نسخه اندروید

پکیج اندرویدی چت را میتوانید از لینک زیر با استفاده از گیت دریافت کنید یا فایل زیپ آن را دانلود نمایید.

لینک گیت هاب

**راهنمای نصب با استفاده از Android Studio:**

چت Sdk به صورت یک ماژول مستقل نیز از طریق maven  قابل دسترس است.

با اضافه کردن در app/build.gradle در قسمت dependencies می توانید نیز به پروژه ی خود اضافه کنید.
  
    dependencies { 
    implementation 'com.fanap.podchat:podchat:0.4.2.0' }
  

**پیش نیاز ها:**

+ دسترسی اینترنت به اپلیکیشن باید داده شود. خط زیر را به فایل AndroidManifest.xml پروژه خود اضافه کنید:
   
    <uses-permission android:name="android.permission.INTERNET" />
   

هر کاربر جهت ورود نیازمند به یک توکن دسترسی است. 
توکن دسترسی باید قبل از استفاده از پکیج چت ، از سرور sso دریافت شود تا به هنگام ساخت نمونه ی اولیه از شیء چت به عنوان پارامتر به آن داده شود.


**ساخت نمونه اولیه:**

اولین قدم ساخت یک شیء نمونه از ماژول چت است.

    chat.init(context);


سپس ارتباط با سرور مانند مثال زیر از طریق متد connect برقرار میشود.


    \* @param requestConnect {
         \*                       socketAddress {**REQUIRED**}
         \*                       platformHost  {**REQUIRED**}
         \*                       severName     {**REQUIRED**}
         \*                       appId         {**REQUIRED**}
         \*                       token         {**REQUIRED**}
         \*                       fileServer    {**REQUIRED**}
         \*                       ssoHost       {**REQUIRED**}
         \*                       }
         \*/
    RequestConnect requestConnect = new RequestConnect
                    .Builder(serverAddress, appId, severName, token, ssoHost, platformHost, fileServer)
                    .build();
            chat.connect(requestConnect);


آدرس ها و تنظیمات

در نهایت نمونه ی ساخته شده آماده ی استفاده است.

با قرار دادن true در لاگ به شما لاگ خام بدون تغییرات را نشان می دهد. توصیه می شود در هنگام توسعه این لاگ را فعال کنید.
  
    chat.rawLog(boolean rawLog);
  

با قرار دادن مقدار زمانی که میخواهید هنگام فرستادن سیگنال هایی مانند _is_typing  هر چند ثانیه سینگال مخصوص را می فرستد.

    	chat.signalIntervalTime(int Second)
   

قابلیت کش را فراهم می کند.

    chat.isCacheables(boolean cache);


لاگ را برای تمام جواب ها و ریکویست ها نشان می دهد.

    chat.isLoggable(boolean log);



## مدیریت مخاطبین

**۱- getContacts:**
دریافت لیست مخاطبین. این متد یک لیست جهت تنظیمات صفحه بندی (حداکثر تعداد مخاطبین در هر درخواست و شماره ی  شروع) دریافت میکند و لیست تمامی مخاطبین کاربر را بازمیگرداند.

    count = 50;
    offset = 0;
    
     RequestGetContact requestGetContact = new RequestGetContact.Builder()
                    .count()
                    .offset()
                    .build();
     chat.getContacts(requestGetContact,null);


**۲- addContact:**

با دریافت نام ، نام خانوادگی ، شماره تماس و ایمیل ، مخاطب جدید ذخیره خواهد کرد.

نکته:
در صورت ارسال مقدار پارامترfirstName برای مخاطب، اجباری به ورود پارامتر نام خانوادگی(و بالعکس) نمی باشد و هم چنین در صورت ورود شماره موبایل، ورود ایمیل الزامی نیست(و بالعکس).

اما توجه داشته باشید ارسال مقادیر پارامتر(اگرچه بدون مقدار ورودی) الزامی می باشد.

      /**
     	\* Add one contact to the contact list
     	\*
     	\* @param request {
     	\*            	firstName   	Notice: if just put fistName without lastName its ok.
     	\*            	lastName    	last name of the contact
     	\*            	cellphoneNumber Notice: If you just  put the cellPhoneNumber doesn't necessary to add email
     	\*            	email       	email of the contact
     	\*            	}
     	\*/
       	  RequestAddContact requestAddContact = new RequestAddContact.Builder()
                	.firstName()
                	.lastName()
                	.cellphoneNumber()
                	.email()
                	.build();
        	chat.addContact(requestAddContact);


**۳- updateContact:**

مشخصات جدید کاربر را به همرا id (همان آیدی مخاطب که پس از ذخیره ، یا به هنگام استفاده از سرویس لیست مخاطبین دریافت کرده اید) در لیست پارامتر ورودی به این متد بدهید تا عملیات تغییر مشخصات مخاطب مورد نظر صورت گیرد. پاسخ مشابه سرویس قبلی خواهد بود. 

    /**
     	\* Update contacts
     	\* All of the params all [Required]
     	\*
     	\* @param request {
     	\*             	String firstName [Required]
     	\*             	String lastName [Required]
     	\*             	String cellphoneNumber [Required]
     	\*             	String email [Required]
     	\*             	long userId [Required]
     	\*            	}
     	\*/
         RequestUpdateContact requestUpdateContact = new RequestUpdateContact.Builder(userId)
                	.firstName()
                	.lastName()
                	.cellphoneNumber()
                	.email()
                	.build();
        	chat.updateContact(updateContact);


**۴- removeContact:**

با دریافت آیدی مخاطب، مشخصات آن را از لیست مخاطبین حذف میکند.

    /**
     	\* Remove contact with the user id
     	\*
     	\* @param request {
     	\*            	long userId
     	\*            	}
     	\*/
       	 RequestRemoveContact requestRemoveContact = new RequestRemoveContact.Builder(userId)
                	.build();
        	chat.removeContact(requestRemoveContact);


**۵- syncContact:** 

تمامی مخاطبین دستگاه را که در لیست مخاطبین اپلیکیشن شما نیستند ، به آن اضافه میکند.

     /**
     	\* First we get the contact from server then at the respond of that
     	\*
     	\* @param activity its for check the permission of reading the phone contact
     	\*             	{@link #getPhoneContact(Context)}
     	\*/
    	chat.syncContact(Activity activity);


**۶-block:**

با دریافت آیدی مخاطب، ایدی ترد  و ایدی کاربری، امکان ارتباط با او را مسدود میکند.

    /**
         \* It blocks the thread
         \* @ param contactId id of the contact
         \* @ param threadId  id of the thread
         \* @ param userId    id of the user
         \*/
    
    	  RequestBlock requestBlock = new RequestBlock.Builder()
                    .contactId()
                    .threadId()
                    .userId()
                    .build();
            chat.block(requestBlock,null);
    	 


**۷-getBlockList:**

لیست مخاطبین بلاک شده را بازمیگرداند.

با پر کردن مقادیر ورودی count و offset میتوانید تنظیمات صفحه بندی را اعمال کنید.

		  /**
     \* It gets the list of the block list
     \*
     \* @param request {
     \*                ----- long count Number of the response
     \*                ----- long offset offset of the response
     \*                }
     \* @param handler Its not useful yet set it to null
     \*/
        RequestBlockList requestBlockList = new RequestBlockList.Builder()
                .count()
                .offset()
                .build();
        chat.getBlockList(requestBlockList,null);


**۸-unblock:**

با دریافت blockId (آیدی مخاطب از لیست مسدود شده ها)، UserId , ContactId, ThreadId امکان ارتباط مجدد با مخاطب را برقرار میکند و مخاطب از لیست مسدود شده ها خارج میشود.


    /**
         \* It unblocks thread with three way
         \*
         \* @ param blockId it can be found in the response of getBlockList
         \* @ param userId Id of the user
         \* @ param threadId Id of the thread
         \* @ param contactId Id of the contact
         \*/ 
    RequestUnBlock requestUnBlock = new RequestUnBlock.Builder()
                    .blockId()
                    .contactId()
                    .threadId()
                    .userId()
                    .build();
            chat.unblock(request, handler);


**۹- searchContact:**

با دریافت پارامترهای زیر، از بین مخاطبین کاربر به جستجو پرداخته و لیستی از مخاطبین با مشخصات داده شده را بازمیگرداند.

پارامترهای ضروری را با استفاده از builder مقدار دهی میشوند ، همچنین هر یک از پارامتر های دلخواه را در صورت وجود به آن اضافه کرده و شیء ورودی متد را به کمک آن بسازید.

    /*
    \*cellphoneNumber
    \*email
    \*firstName
    \*lastName
    \*uniqueId
    \*id
    \*offset 
    \*size 
    \*typeCode
    \*q
    \*/
    
    SearchContact searchContact = new SearchContact.Builder(string offset, string size).id(string id).build();
    
    chat.searchContact(SearchContact searchContact);



### مدیریت تردها

**۱- getThreads:**

لیست تمام ترد های اخیرا ایجاد شده ی کاربر را به ترتیب زمانی و بر اساس متغیر های صفحه بندی (count, offset) نشان خواهد داد.

    /**
         \*
         \* @param creatorCoreUserId    if it sets to '0' its considered as it was'nt set   Optional]
         \* @param partnerCoreUserId    if it sets to '0' its considered as it was'nt set -
         \*                             it gets threads of p2p not groups   Optional]
         \* @param partnerCoreContactId if it sets to '0' its considered as it was'nt set-
         \*                             it gets threads of p2p not groups   Optional]
         \* @param count                Count of the list   Optional]
         \* @param offset               Offset of the list  [Optional]
         \* @param handler               Its not working yet set it to null [Optional]
         \* @param threadIds             List of thread ids that you want to get  [Optional]
         \* @param threadName            Name of the thread that you want to get  [Optional]
         \*/
    
    RequestThread requestThread = new RequestThread.Builder()
    .partnerCoreContactId()
    .threadIds()
    .threadName()
    .partnerCoreContactId()
    .creatorCoreUserId()
    .partnerCoreUserId()
    .count()
    .offset()
    .build();
    
    getThreads(requestThread , null)


**۲- getHistory:**

با دریافت آیدی مربوط به یک ترد ، تاریخچه ی آن را بر اساس تنظیمات صفحه بندی (count,offset) نشان خواهد داد.

    /**
         \* Gets history of the thread
         \*
         \* @Param count    count of the messages  [Optional]
         \* @Param order    If order is empty [default = desc] and also you have two option [ asc | desc ]       [Optional]
         \* @Param long threadId   Id of the thread 
         \* @Param long fromTime    Start Time of the messages  [Optional]
         \* @Param long fromTimeNanos  Start Time of the messages in Nano second  [Optional]
         \* @Param long toTime         End time of the messages  [Optional]
         \* @Param long toTimeNanos    End time of the messages  [Optional]
         \* @Param @Deprecated long firstMessageId
         \* @Param @Deprecated long lastMessageId
         \*
         \* <p>
         \* threadId Id of the thread that we want to get the history
         \*/
    
    RequestGetHistory requestGetHistory = new RequestGetHistory.Builder(threadId)
                    .fromTime()
                    .fromTimeNanos()
                    .id()
                    .toTime()
                    .toTimeNanos()
                    .build();
    chat.getHistory(requestGetHistory , null)


**۳- createThread:**

ساخت یک ترد ، شامل ساخت ترد نفر به نفر (چت دو نفره) ، یا ترد جمعی (گروه) می باشد. در حالت عادی نحوه ی ایجاد هر دو مدل یکسان است ، تفاوت در تعداد نفرات گروه نسبت به ترد دو نفره میباشد.

    /*available thread types*/
    /*  int NORMAL = 0; 
     \*  int OWNER_GROUP = 1; 
     \*  int PUBLIC_GROUP = 2; 
     \*  int CHANNEL_GROUP = 4; 
     \*  int CHANNEL = 8;
    \*/
    
    /*available invitee types*/
    /*int TO_BE_USER_SSO_ID = 1; 
     \*int TO_BE_USER_CONTACT_ID = 2; 
     \*int TO_BE_USER_CELLPHONE_NUMBER = 3; 
     \*int TO_BE_USER_USERNAME = 4;
     \*TO_BE_USER_ID = 5  // just for p2p
    \*/
    
    Invitee[] invt = new Invitee[]{new Invitee(485, 2)};
    chat.createThread(threadType, invt, threadTitle);`...`


**۴- muteThread**

با دریافت آیدی ترد ، ترد مربوطه را mute میکند.


**۵- unmuteThread**

با دریافت آیدی ترد  ، مشخصه ی mute ترد مربوطه را در صورت فعال بودن ، غیرفعال میکند.

نکته: mute و unmute جهت غیرفعال و فعال کردن نوتیفیکیشن یک ترد کاربرد دارد.

    /**
     	\* Mute the thread so notification is off for that thread
     	\* @param request {
     	\*            	long threadId : id of the thread
     	\* }
     	\* @param handler : its not useful yet. set it to null
     	\*/
       	 RequestMuteThread requestMuteThread = new RequestMuteThread.Builder()
                	.threadId(threadId)
                	.build();
        	chat.muteThread(requestMuteThread);
    
        	/**
     	\* It Un mutes the thread so notification is off for that thread
     	\*
     	\* @param request {
     	\*            	long threadId : id of the thread
     	\*            	}
     	\* @param handler : its not useful yet. set it to null
     	\*/
         RequestMuteThread muteThread = new RequestMuteThread.Builder()
                	.threadId(threadId)
                	.build();
        	chat.unMuteThread(muteThread,null);


**۶- getThreadParticipants:**

با دریافت آیدی ترد و تنظیمات صفحه بندی ، اعضای آن ترد را نشان میدهد. به عنوان ورودی دوم میتوان به این متد یک callback اختصاص داد تا پس از پاسخ سرور اجرا شود.

    	/**
         \* Get the participant list of specific thread
         \* <p>
         \*
         \* @ param long threadId id of the thread we want to get the participant list
         \* @ param long count number of the participant wanted to get
         \* @ param long offset of the participant list
         \*/
    
    RequestThreadParticipant participant = new RequestThreadParticipant.Builder(threadId)
                    .count()
                    .offset()
                    .build();
    chat.getThreadParticipants(participant ,null)


**۷- addParticipants:**

با دریافت آیدی ترد و لیستی از از آیدی مخاطبین (contact Id) ، آنها را به اعضای ترد مربوطه اضافه میکند.

    /**
     	\* contactIds  List of CONTACT IDs
     	\* threadId   Id of the thread that you are {*NOTICE*}admin of that and you are going to
     	\* add someone as a participant.
     	\*
     	\* @param request {
     	\*            	long threadId : Id of the thread
     	\*            	List<Long> contactIds : list of contact ids that wanted to be add
     	\*            	}
     	\* @param handler : its not useful yet. set it to null
     	\*/
       	  RequestAddParticipants addParticipants = new RequestAddParticipants
                	.Builder(threadId,contactIds)
                	.build();
        	chat.addParticipants(requestAddParticipants, null);


**۸- removeParticipants:**

با دریافت آیدی ترد و لیستی از آیدی کاربران (userId)، آنها را از ترد مورد نظر حذف میکند.

     /**
         \* @param request {
         \*                participantIds :  List of PARTICIPANT IDs from Thread's Participants object
         \*                threadId      : Id of the thread that we wants to remove their participant
         \*                }
         \* @param handler it should be null
         \*/
    RequestRemoveParticipants removeParticipants = new RequestRemoveParticipants
                    .Builder(threadId,participantsId)
                    .build();
    
            chat.removeParticipants(requestRemoveParticipants, handler);


**۹- leaveThread:**

با دریافت آیدی ترد ، کاربر را از ترد مربوطه خارج میکند.

    /**
         \* leaves the thread
         \*
         \* @param request{ threadId id of the thread
         \*                 }
         \* @param handler it should be null
         \*/
    RequestLeaveThread leaveThread = new RequestLeaveThread.Builder(threadId)
                    .build();
            chat.leaveThread(leaveThread,null);

**10- "createThreadWithMessage"**

ساخت یک ترد ، شامل ساخت ترد نفر به نفر (چت دو نفره) ، یا ترد جمعی (گروه) می باشد. در حالت عادی نحوه ی ایجاد هر دو مدل یکسان است ، تفاوت در تعداد نفرات گروه نسبت به ترد دو نفره میباشد.

    {
      'hasError:' false,
      'errorMessage:' '',
      'errorCode:' 0,
      'result:' {
        'thread:' {
          'id:' 82,
          'joinDate:' undefined,
          'title:' undefined,
          'inviter:' undefined,
          'participants:' undefined,
          'time:' undefined,
          'lastMessage:' undefined,
          'lastParticipantName:' undefined,
          'group:' undefined,
          'partner:' undefined,
          'image:' undefined,
          'unreadCount:' undefined,
          'lastMessageId:' undefined,
          'lastMessageVO:' undefined,
          'partnerLastMessageId:' undefined,
          'partnerLastDeliveredMessageId:' undefined,
          'type:' undefined,
          'metadata': undefined,
          'mute:' undefined,
          'participantCount:' undefined,
          'canEditInfo:' undefined
        }
      }
    }


**11 - "updateThreadInfo"**

با در یافت اطلاعات ترد آن را اپدیت می کند البته باید در نظر داشت که اطلاعاتی هم که لازم به اپدیت نیست فرستاده شود در غیر اینصورت آن فیلد ها خالی اپدیت می شوند.

	    /**
     	\* It updates the information of the thread
     	\* @param request {
     	\*            	String image : image of the thread
     	\*            	long threadId : Id of the thread
     	\*            	String name : Name of the thread
     	\*            	String description : Description of the thread
     	\*            	String metadata : Metadata of the thread
     	\*            	}
     	\* @param handler Its not useful yet.
     	\*          	 
     	\*/
         RequestThreadInfo threadInfo = new RequestThreadInfo.Builder()
                	.threadId()
                	.description()
                	.image()
                	.metadat()
                	.name()
                	.build();
        	chat.updateThreadInfo(request, null);



### مدیریت پیام ها

**۱- sendTextMessage:**

ارسال پیام به یک ترد، با دریافت آیدی ترد و پیغام ارسالی. پس از ارسال پیغام، سه رویداد قابل رخداد است:

1.  "onSent": که رویداد پس از ارسال پیغام است و توسط سرور به فرستنده اعلام میشود.
2.  "onDeliver": پس از تحویل پیغام به گیرنده، سرور به صورت خودکار وضعیت دریافت شدن پیغام توسط گیرنده را به وسیله رویداد onDeliver اعلام میکند.
3.  "onSeen": اعلام وضعیت پیام دیده شده باید توسط دریافت کننده ی پیام ، از طریق فراخوانی متد seen توسط دریافت کننده صورت گیرد.سرور پیام رسان به محض دریافت این اطلاعیه ، آن را از طریق رویداد onSeen به اطلاع فرستنده میرساند.


    textMessage = "your text message."; //Required
    threadId = 83; //Required
    
    /**
         \* Its sent message but it gets Object as an attribute
         \*
         \* @param requestMessage {
         \*                       String textMessage : text of the message
         \*                       int messageType : type of the message
         \*                       String jsonMetaData : metadata of the message
         \*                       long threadId : The id of a thread that its wanted to send
         \*                       }
         \* @param handler        @param handler Its not useful yet.set it to null
         \*/	
    RequestMessage message = new RequestMessage
                    .Builder(textMessage,threadId)
                    .build();
    chat.sendTextMessage(requestMessage, null);


**۲- editMessage:**

با دریافت آیدی پیغام و متن جدید پیغام ، پیغام مربوطه را تغییر میدهد.

نکته: سرور نتیجه ی تغییر پیغام را بر روی رویداد "_onEditedMessage_" گزارش خواهد داد.

    messageId = 514; //Required
    messageContent = "edited message"; //Required
    
    /**
     	\* Message can be edit when you pass the message id and the edited
     	\* content in order to edit your Message.
     	\*
     	\* @param request {
     	\*            	String messageContent : content of them message
     	\*            	long messageId : id of the message it wanted to be edit
     	\*            	String metaData : metaData of the message
     	\*            	}
     	\* @param handler : its not useful yet. set it to null  
     	\*/
       	 equestEditMessage editMessage = new RequestEditMessage.
                	Builder(messageContent,messageId)
                	.metaData()
                	.build();
        	chat.editMessage(editMessage,null);


**۳- replyMessage:**

با دریافت آیدی ترد ، آیدی پیام ، و محتوای دلخواه ، پیام مورد نظر شما را انتخاب و محتوا را در پاسخ به آن پیام ارسال میکند.

با توجه به اینکه جنس این متد همانند sendTextMessage از نوع ارسال پیام است ، در نتیجه سه callback جهت عملیات پس از ارسال، دریافت، و دیده شدن پیام لازم خواهد داشت.

    threadId = threadId; //Required
    repliedTo = messageId; //Required
    content = message; //Required
    
    	  /**
     	\* Reply the message in the current thread and send az message and receive at the
     	\* <p>
     	\*
     	\* @param request{ messageContent content of the reply message
     	\*             	threadId   	id of the thread
     	\*             	messageId  	message id of the message that we want to reply
     	\*             	metaData   	meta data of the message
     	\*             	}
     	\* @param handler : its not useful yet. set it to null
     	\*/
       		      	RequestReplyMessage requestReplyMessage = new RequestReplyMessage
                	.Builder(messageContect,threadId,messageId)
                	.messageType()
                	.systemMetaData()
                	.build();
        	chat.replyMessage(request, handler);


**۴- forwardMessage:**

این متد ، باز ارسال یک پیام انتخابی را به یک ترد مشخص، با استفاده از آیدی پیام (جهت انتخاب آن) و آیدی ترد مقصد انجام خواهد داد. نوع این متد نیز ارسال پیام است.

    /* Required fields */
    /*  threadId 
     \*  messageIds
    \*/
    
     /**
     	\* forward message to some thread
     	\*
     	\* @param request {
     	\*            	threadId : destination thread id
     	\*            	messageIds : List of message ids that we want to forward them
     	\*            	}
     	\*/
       	 RequestForwardMessage requestForwardMessage = new RequestForwardMessage
                	.Builder(threadId,messageIds)
                	.build();
        	chat.forwardMessage(request);


نکته: متد باز ارسال لیستی از پیام ها را با دریافت آیدی پیام ها به ترد مقصد ارسال میکند. در این حالت برای هر پیام یک uniqueId جداگانه خواهد بود.


**۵- sendFileMessage:**

ارسال پیام با محتوای فایل به یک ترد مشخص. با دریافت آیدی ترد مقصد، آدرس فایل مورد نظر، محتوای متن همراه عکس و محتوای مورد نظر متادیتا، فایل ارسالی را پس از آپلود بر روی سرور، به همراه پیام ارسالی به ترد مقصد ارسال میکند.

    /* Required fields */
     \*  threadId
     \*  fileUri
    \*/
    
    /**
     	\* This method first check the type of the file and then choose the right
     	\* server and send that
     	\* <p>
     	\*
     	\* @param requestFileMessage {description	Its the description that you want to send with file in the thread
     	\*                        	fileUri    	Uri of the file that you want to send to thread
     	\*                        	threadId   	Id of the thread that you want to send file
     	\*                        	systemMetaData [optional]}
     	\* @param handler        	handler    	it is for send file message with progress
     	\*/
         RequestFileMessage fileMessage = new RequestFileMessage.
                	Builder(activity,threadId,fileUri)
                	.messageType()
                	.systemMetadata()
                	.build();
    
    
        	chat.sendFileMessage(requestFileMessage, handler);


**۶- deleteMessage:**

با دریافت آیدی پیام (messageId) ، پیام مربوطه را حذف خواهد کرد.

نکته: در صورتی که متغیر deleteForAll را با مقدار true پر کنید ، پیام مذکور از تاریخچه ی ترد همه ی اعضای آن ترد پاک خواهد شد.

    /* Required fields */
    /*  messageId 
    \*/
    
    /**
     	\*
     	\* @param request {
     	\*             	ArrayList<Long> messageIds;
     	\*             	boolean deleteForAll : If you want to delete message for everyone you can set it true if u don't want
     	\* you can set it false 
     	\*            	}
     	\* @param handler : its not useful yet. set it to null
     	\*/
       	  RequestDeleteMessage requestDeleteMessage = new RequestDeleteMessage.Builder()
                	.messageIds()
                	.deleteForAll()
                	.build();
        	chat.deleteMessage(deleteMessage, handler);


7 - **"replyFileMessage"**:

پاسخ پیام با محتوای فایل به یک ترد مشخص. با دریافت آیدی ترد مقصد، آدرس فایل مورد نظر، محتوای متن همراه عکس و محتوای مورد نظر متادیتا، فایل ارسالی را پس از آپلود بر روی سرور، به همراه پیام ارسالی به ترد ارسال میکند.

    /**
     	\* Reply the message in the current thread and send az message and receive at the
     	\* <p>
     	\* messageContent content of the reply message
     	\* threadId   	id of the thread
     	\* messageId  	of the message that we want to reply
     	\* metaData   	meta data of the message
     	\*
     	\* @param request {
     	\*            	String messageContent : content of the reply message
     	\*            	long threadId : id of the thread
     	\*            	long messageId : message id of the message that wanted to be reply
     	\*            	String systemMetaData : meta data of the message
     	\*            	Uri fileUri : Uri of the file
     	\*            	Activity activity
     	\*            	int messageType : Type of the message
     	\*            	}
     	\* @param handler
     	\*/
         RequestReplyFileMessage replyFileMessage = new RequestReplyFileMessage
        	.Builder(messageContent,threadId,messageId,fileUri,activity)
        	.messageType()
        	.systemMetaData()
        	.build();
             	chat.replyFileMessage(request, handler);


8 - **"getMessageSeenList"**:

گرفتن لیست کسانی که مسیج را دیده اند.

      /**
     	\* Gets the list of the participant that the message is seen
     	\*
     	\* @param requestParams {
     	\*                  	long messageId : Id of the message
     	\*                  	}
     	\*/
       	  RequestSeenMessageList seenMessageList = new RequestSeenMessageList
                	.Builder(messageId)
                	.build();
        	chat.getMessageSeenList(seenMessageList);


9- **"getMessageDeliveredList"**:

گرفتن لیست کسانی که مسیج به آنها رسیده است.

    /**
     	\* Gets the list of the person that the message has been delivered to them
     	\*
     	\* @param requestParams {
     	\*                  	long messageId : Id of the message
     	\*                  	}
     	\*/    
       	  RequestDeliveredMessageList requestDeliveredMessageList = new RequestDeliveredMessageList
                	.Builder(messageId)
                	.build();
        	chat.getMessageDeliveredList(requestDeliveredMessageList);


10- **"resendMessage"**:

فرستادن مسیجی که درصف مانده است.

    /**
     	\* If you want to resend the message that is stored in waitQueue
     	\*
     	\* @param uniqueId the unique id of the waitQueue message
     	\*/
       	 chat.resendMessage(uniqueId);


11 - **"cancelMessage"**:

کنسل کردن مسیج که در صف مانده است.

     /**
     	\* It cancels message if its still in the Queue
     	\*/
    	chat.cancelMessage(uniqueId);



### مدیریت فایل ها

**۱- uploadImage:** 

با دریافت آدرس فایل عکس ، آن را بر روی سرور فایل ذخیره میکند.

نکته:پارامترهای context و activity جهت دسترسی به ریسورس های دستگاه و بررسی دسترسی های موجود لازم است.

    chat.uploadImage(Context context, Activity activity, Uri fileUri);
    
    RequestUploadImage requestUploadImage = new RequestUploadImage.Builder(activity,fileUri)
                    .build();
    
    chat.uploadImage(requestUploadImage);


**۲- getImage:**

با دریافت آیدی تصویر ذخیره شده و کد مشخصه ی آن (hashCode) لینک دریافت آن را در اختیار قرار میدهد.

     chat.getImage(imageId ,hashCode);
    
            RequestGetImage requestGetImage = new RequestGetImage
                    .Builder(imageId,hashCode,downloadable)
                    .build();
            chat.getImage(requestGetImage);


**۳- uploadFile:**

با دریافت آدرس فایل آن را در سرور فایل بارگذاری خواهد کرد.

    /**
         \* @param requestUploadFile {
         \*                          Activity activity
         \*                          Uri fileUri : Uri of the file
         \*                          }
         \*/		
    RequestUploadFile uploadFile = new RequestUploadFile.Builder(activity, uri)
                    .build();
            chat.uploadFile(uploadFile);



**۴- getFile:**

با دریافت آیدی فایل ذخیره شده و کد مشخصه ی آن (hashCode) لینک آن را در اختیار قرار میدهد.این متد پارامتری به عنوان downloadable دارد که از نوع boolean است. در صورت مثبت بودن لینک فایل خروجی قابل دانلود خواهد بود.

    RequestGetFile requestGetFile = new RequestGetFile
                    .Builder(fileId,hashCode,downloadable)
                    .build();
            chat.getFile(requestGetFile);


**"uploadImageProgress"**:

با استفاده از این متد می توانید مقدار بایتی را که در حال آپلود شدن است را با استفاده از اینترفیس ProgressHandler.onProgress دنبال کنید.  

    	 /**
         \* @param requestUploadImage {
         \*                           Activity activity
         \*                           Uri fileUri : Uri of the file
         \*                           }
         \* @param handler            It has 3 listener{
         \*                           onProgressUpdate(String uniqueId, int bytesSent, int totalBytesSent, int totalBytesToSend)
         \*                           onError(String jsonError, ErrorOutPut error)
         \*                           onFinish(String imageJson, ChatResponse<ResultImageFile> chatResponse)
         \*                           }
         \*/
    RequestUploadImage requestUploadImage = new RequestUploadImage.Builder(activity,fileUri)
                    .build();
            chat.uploadImageProgress(requestUploadImage, new ProgressHandler.onProgress() {
                @Override
                public void onProgressUpdate(String uniqueId, int bytesSent, int totalBytesSent, int totalBytesToSend) {
    
                }
    
                @Override
                public void onFinish(String imageJson, ChatResponse<ResultImageFile> chatResponse) {
    
                }
    
                @Override
                public void onError(String jsonError, ErrorOutPut error) {
    
                }
            });


**"uploadFileProgress"**:

با استفاده از این متد می توانید مقدار بایتی را که در حال آپلود شدن است را با استفاده از اینترفیس ProgressHandler.onProgress دنبال کنید.

    /**
         \* It uploads file and it shows progress of the file downloading
         \*
         \* @param requestUploadFile {
         \*                          Activity activity
         \*                          Uri fileUri
         \*                          }
         \* @param handler           {
         \*                          onProgress
         \*                          onFinish
         \*                          onError
         \*                          }
         \*/
    	  RequestUploadFile uploadFile = new RequestUploadFile.Builder(activity, uri)
                    .build();
    
            chat.uploadFileProgress(uploadFile, new ProgressHandler.onProgressFile() {
                @Override
                public void onFinish(String imageJson, FileUpload fileImageUpload) {
    
                }
    
                @Override
                public void onError(String jsonError, ErrorOutPut error) {
    
                }
    
                @Override
                public void onProgress(String uniqueId, int bytesSent, int totalBytesSent, int totalBytesToSend) {
    
                }
    
            });


### مدیریت پروفایل

**۱- getUserInfo:**

این متد اطلاعات پروفایل کاربر را در اختیارش قرار میدهد. با توجه به توکن دسترسی عمل میکند، لذا نیازی به ورودی ندارد.


    chat.getUserInfo(null);


    //output:
    
    {
      "hasError": false,
      "errorMessage": null,
      "errorCode": 0,
      "result": {
        "user": {
          "id": 41,
          "name": "محمد واحدی",
          "email": null,
          "cellphoneNumber": "0937******6",
          "image": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=1310&width=178&height=178&hashCode=162d76c669f-0.4826280911609194",
          "lastSeen": null,
          "sendEnable": true,
          "receiveEnable": true
        }
      }
    }



### موقعیت و مسیریابی

**۱- mapSearch:**

نام خیابان، اماکن و کسب و کار های ثبت شده و ... (searchTerm) را حول نقطه ی مرجع (مختصات طول و عرض جغرافیایی مرجع با متغیرهای latitude , longitude مشخص میشود) جستجو میکند.

    chat.mapSearch(String searchTerm, Double latitude, Double longitude);


    {
      "errorCode": 0,
      "errorMessage": null,
      "result": {
        "maps": [
          {
            "region": "تهران",
            "title": "میدان آزادی",
            "category": "place",
            "type": "roundabout",
            "location": {
              "z": "NaN",
              "y": 35.69972390081852,
              "x": 51.33750630393097
            },
            "address": "میدان آزادی - تهران",
            "neighbourhood": "آپادانا"
          },
          .
          .
          .
          {
            "region": "تهران",
            "title": "ایستگاه مترو میدان آزادی",
            "category": "place",
            "type": "subway_station",
            "location": {
              "z": "NaN",
              "y": 35.701164,
              "x": 51.3332562
            },
            "address": "آپادانا، بزرگراه لشگری - تهران",
            "neighbourhood": "آپادانا"
          }
        ]
      },
      "count": 29,
      "hasError": false
    }


**۲- mapRouting:**

با دریافت دو مختصات مبدا و مقصد بهترین مسیر بین دو نقطه‌ی مشخص را با توجه به ترافیک معابر محاسبه می کند و هر پاسخ ممکن است شامل یک یا چند مسیر باشد. در هر مسیر زمان سفر و مسافت آن محاسبه می‌گردد. مرتب‌سازی مسیرها بر اساس بهترین مسیر از نظر زمان و مسافت خواهد بود.

اولین پارامتر ورودی مختصات نقطه شروع مسیریابی، یا همان مبدا است (origin)، این مختصات باید به صورت latitude,longitude باشد که دو عدد با کاما از هم جدا شده‌اند.دومین پارامتر ورودی مقصد است (destination) که مختصات نقطه پایان مسیریابی و قالب آن مانند نقطه شروع است.

    chat.mapRouting(String origin, String destination);


    {
      "errorCode": 0,
      "errorMessage": null,
      "result": {
        "routes": [
          {
            "legs": [
              {
                "summary": "بزرگراه شهریار - بویین زهرا - ",
                "duration": {
                  "value": 5941,
                  "text": "۱ ساعت ۳۹ دقیقه"
                },
                "distance": {
                  "value": 101358,
                  "text": "۱۲۵ کیلومتر"
                },
                "steps": [
                  {
                    "instruction": "در جهت غرب در میدان آزادی قرار بگیرید",
                    "distance": {
                      "value": 238,
                      "text": "۲۵۰ متر"
                    },
                    "start_location": [
                      51.337639,
                      35.70078
                    ],
                    "name": "میدان آزادی"
                  },
                  {
                    "instruction": "به مسیر خود ادامه دهید",
                    "distance": {
                      "value": 76,
                      "text": "۱۰۰ متر"
                    },
                    "start_location": [
                      51.335338,
                      35.70004
                    ],
                    "name": ""
                  },
                  .
                  .
                  .
                  {
                    "instruction": "در مقصد قرار دارید",
                    "distance": {
                      "value": 0,
                      "text": "۰ متر"
                    },
                    "start_location": [
                      50.327996,
                      35.734918
                    ],
                    "name": ""
                  }
                ]
              }
            ],
            "overviewPolyline": ""
          }
        ]
      }
    }



### "Event Listeners"

جهت دسترسی به هر یک از این event ها باید به این صورت عمل کنید:

    chat.addListener(new ChatAdapter() {
                @Override
                public void onSeen(String content) throws IOException {
                    super.onSeen(content);
                }
            });

یا کلاس خود را از ChatAdapter ارث بری کنید:

    public class MyActivity extends ChatAdapter {
    .
    .
    .
        @Override
        public void onSeen(String content) throws IOException {
            Log.d("RAW_MESSAGE", content);
            super.onSeen(content);
            .
            .
            .
         }
    .
    .
    }



### آدرس ها و تنظیمات

تنظیمات و آدرس های زیر برای اتصال Async (به روی سرور سندباکس) باید به عنوان پارامتر ورودی پس از ساخت نمونه ی اولیه از پکیج، به متد connect داده شود تا اتصال با سرور انجام گیرد.

     socketServerAddress = "wss://chat-sandbox.pod.land/ws", // {*REQUIRED*} Socket Server Address
      ssoHost = "https://accounts.pod.land", // {*REQUIRED*} SSO Server Address
      platformHost = "https://sandbox.pod.land:8043/srv/basic-platform", // {*REQUIRED*} Platform Server Address
      fileServer = "http://sandbox.fanapium.com:8080", // {*REQUIRED*} File Server Address
      serverName = "chat-server", // {*REQUIRED*} Server to register on
      token = "CLIENT_ACCESS_TOKEN", // {*REQUIRED*} SSO Token
    
    chat.connect(socketServerAddress, appId, serverName, token , ssoHost, platformHost, fileServer)


## نصب- نسخه iOS

پکیج iOS چت را میتوانید با استفاده از لینک زیر، از گیت هاب دریافت کنید.

لینک گیت هاب


**راهنمای نصب و استفاده در Xcode**

پروژه ی خود را در Xcode باز کنید.

پکیج دانلود شده را روی پروژه ی خود، بصورت drag and drop بکشید.

دقت کنید که تیک گزینه ی Copy items if needed رو فعال کرده، سپس Finish را بزنید.

در قسمت Navigator ، پروژه ی خود را انتخاب کنید.

تب Build Phases را باز کنید.

منوی Link Binary With Libraries را انتخاب کنید.

گزینه ی + را کلیک کنید.

پکیج Chat.framework را پیدا کرده و Add کنید.

دقت کنید که باید دستور زیر را در ابتدای سورس کد خود اضافه کنید:

```
import FanapPodChatSDK
```



**پیش نیاز ها:**

ابتدا باید اجازه ی دسترسی درخواست های HTTP به به اپلیکیشن داده شود.

Navigator -> Info.plist (right-click) -> Open As -> Source Code

حالا کد زیر را اضافه کرده و به جای عبارت “YourDomainName” ، آدرس دامین خود را (که درخواست های HTTP به آن زده میشوند) جایگذاری کنید.

    <key>NSAppTransportSecurity</key>
        <dict>
    	<key>NSAllowsArbitraryLoads</key>
    	<true/>
    	<key>NSExceptionDomains</key>
    	<dict>
    	    <key>YourDomainName</key>
    	    <dict>
    		<key>NSExceptionAllowsInsecureHTTPLoads</key>
    		<true/>
    		<key>NSIncludesSubdomains</key>
    		<true/>
    	    </dict>
    	</dict>
        </dict>


هر کاربر جهت ورود نیازمند به یک توکن دسترسی است.

توکن دسترسی باید قبل از استفاده از پکیج چت، از سرور sso دریافت شود تا هنگام ساخت نمونه ی اولیه از شیء چت، به عنوان پارامتر به آن داده شود.


**ساخت نمونه اولیه:**

اولین قدم، ساخت یک شیء ، از ماژول چت است.

ابتدا یک property برای نگهداری شیء از چت می سازید:

    var myChatObject: Chat?

سپس چت را با استفاده از پارامتر های ورودی مورد نیاز (آدرس ها و تنظیمات) بسازید:

```
myChatObject = Chat(پارامتر های ورودی مورد نیاز را در این جا باید قرار دهید)
```



مثال:


    myChatObject = Chat(socketAddress:		String,		// Socket Address
                         ssoHost:			String,		// SSO Host Address
                         platformHost:		String,		// PlatForm Address
                         fileServer:		String,		// File Server Address
                         serverName:		String,		// name of your chat server
                         token:			String,		// user TOKEN
                         mapApiKey:			String?,	// 
                         mapServer:			String,		// Map Server Address
                         typeCode:			String?,	// 
                         enableCache:		Bool,		// Do you want to use cache?
                         cacheTimeStampInSec:	Int?,		// How long does the participant objects lives on the Cache
                         msgPriority:		Int?,		//
                         msgTTL:			Int?,		//
                         httpRequestTimeout:	Int?,		//
                         actualTimingLog:		Bool?,		//
                         wsConnectionWaitTime:	Double,		//
                         connectionRetryInterval:	Int,		//
                         connectionCheckTimeout:	Int,		//
                         messageTtl:		Int,		//
                         reconnectOnClose:		Bool)		// Do you want to reconnect if connection lost?


بعد از ساختن چت، باید ChatDelegates را به انتهای تعریف کلاس خود اضافه کنید.

سپس این خط را به کد خود اضافه کنید:

```
myChatObject?.delegate = self
```



حالا باید متدهای ضروری ChatDelegates را پیاده سازی کنید:


    func chatConnected() {
            // do your implementation
        }
    
        func chatReconnect() {
            // do your implementation 
        }
    
        func chatThreadEvents() {
            // do your implementation
        }
    
        func chatReady() {
            // do your implementation 
        }
    
        func chatError(errorCode: Int, errorMessage: String, errorResult: Any?) {
            // do your implementation
        }
    
        func chatState(state: Int) {
            // do your implementation
        }
    
        func chatDeliver(messageId: Int, ownerId: Int) {
            // do your implementation
        }
    
        func messageEvents(type: String, result: JSON) {
            // do your implementation
        }
    
        func threadEvents(type: String, result: JSON) {
            // do your implementation
        }



### مدیریت پروفایل

**۱- getUserInfo:**

این متد اطلاعات پروفایل کاربر را در اختیارش قرار میدهد.

_ورودی:_

با توجه به توکن دسترسی عمل میکند، لذا نیازی به ورودی ندارد.

_خروجی:_

در خروجی این متد، ۳ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، جواب سرور به درخواست کاربر را بصورت مدل UserInfoModel بازمیگرداند.

سومی هم جواب بلادرنگی است که از Cache بازگشت داده میشود.

مثالی از فراخوانی این متد:

    // Request
    // an example of getUserInfo request:
    
    // this is the model that you have to create to pass it through the "getUserInfo" method
    Chat.sharedInstance.getUserInfo(uniqueId: { (getUserInfoUniqueId) in
      // "getContactUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (userInfoServerResponse) in
      // this response is of type "UserInfoModel" but you have to froce cast it as below
      let myResponseModel: UserInfoModel = userInfoServerResponse as! UserInfoModel
    
    }, cacheResponse: { (userInfoCacheResponse) in
      // this it the cache response of this request
      // output of this response, is of type "UserInfoModel". (there is no need to cast is as sth...)
    })



### مدیریت مخاطبین

**۱- getContacts:**

دریافت لیست مخاطبین.

این متد یک لیست جهت تنظیمات صفحه بندی (حداکثر تعداد مخاطبین در هر درخواست و شماره ی  شروع) دریافت میکند و لیست تمامی مخاطبین کاربر را بازمیگرداند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس GetContactsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد getContacts . 

خروجی:

در خروجی این متد، ۳ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، لیست تمامی مخاطبین کاربر را بصورت مدل GetContactsModel بازمیگرداند.

سومی، جواب بلادرنگی است که کاربر درصورت فعال کردن گزینه ی استفاده از Cache، از دیتابیس داخلی خود دریافت میکند. (بعد از دریافت جواب سرور، این دیتابیس بصورت خودکار آپدیت میشود)

مثالی از فراخوانی این متد:

    // Request
    // an example of getContact request:
    
    // this is the model that you have to create to pass it through the "getContacts" method
    let inputModel = GetContactsRequestModel(count:     5,    //
                                             offset:    0,    //
                                             query:     nil,  //
                                             typeCode:  nil,  //
                                             uniqueId:  nil)  //
    
    Chat.sharedInstance.getContacts(getContactsInput: inputModel, uniqueId: { (getContactUniqueId) in
      // "getContactUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (getContactsServerResponse) in
      // this response is of type "GetContactsModel" but you have to froce cast it as below
      let myResponseModel: GetContactsModel = getContactsResponse as! GetContactsModel
    
    }, cacheResponse: { (getContactsCacheResponse) in
      // this it the cache response of this request
      // output of this response, is of type "GetContactsModel". (there is no need to cast is as sth...)
    })


**۲- searchContact:**

جستجو در لیست مخاطب ها.

با دریافت پارامترهای زیر، از بین مخاطبین کاربر به جستجو پرداخته و لیستی از مخاطبین با مشخصات داده شده را بازمیگرداند.

_ورودی:_

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس SearchContactsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد searchContacts .

_خروجی:_

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، پاسخ درخواست جستجو مخاطب ها را بصورت مدل GetContactsModel بازمیگرداند.

سومی، جواب بلادرنگی است که کاربر درصورت فعال کردن گزینه ی استفاده از Cache، از دیتابیس داخلی خود دریافت میکند. (بعد از دریافت جواب سرور، این دیتابیس بصورت خودکار آپدیت میشود)

مثالی از فراخوانی این متد:

    // Request
    // an example of searchContact request:
    
    // this is the model that you have to create to pass it through the "searchContact" method
    let inputModel = SearchContactsRequestModel(cellphoneNumber: "09368640180", //
                                                email:            nil,	        //
                                                firstName:        nil,	        //
                                                id:               nil,	        //
                                                lastName:         nil,	        //
                                                offset:           nil,	        //
                                                size:             nil,	        //
                                                uniqueId:         nil)	        //
    
    Chat.sharedInstance.searchContacts(searchContactsInput: inputModel, uniqueId: { (searchContactsUniqueId) in
    	// "searchContactsUniqueId" is uniqueId of this request, that sends back to client as a callback
    	// do whatever you want with this unique Id
    
    }, completion: { (serverResponse) in
    	// this response is of type "GetContactsModel" but you have to froce cast it as below
    	let myResponseModel: GetContactsModel = serverResponse as! GetContactsModel
    
    }, cacheResponse: { (cacheResponse) in
    	// this it the cache response of this request
    	// output of this response, is of type "GetContactsModel". (there is no need to cast is as sth...)
    })


**۳- addContact:**

اضافه کردن مخاطب جدید.

این متد با دریافت نام ، نام خانوادگی ، شماره تماس و ایمیل، مخاطب جدیدی را ذخیره خواهد کرد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس AddContactsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد addContacts .

نکته: برای ساختن مدل AddContactsRequestModel، در صورت ارسال مقدار پارامترfirstName برای مخاطب، اجباری به ورود پارامتر نام خانوادگی(و بالعکس) نمی باشد؛ و هم چنین در صورت ورود شماره موبایل، ورود ایمیل الزامی نیست(و بالعکس).

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی هم، جواب درخواست ساخت مخاطب جدید را بصورت مدل ContactModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of addContact request:
    
    // this is the model that you have to create to pass it through the "addContacts" method
    let inputModel = AddContactsRequestModel(cellphoneNumber:  "0935****350", //
                                             email:            nil,           // 
                                             firstName:        "Mahyar",      //
                                             lastName:         "Akbarian",    //
                                             uniqueId:         nil)           //
    
    Chat.sharedInstance.addContact(addContactsInput: inputModel, uniqueId: { (addContactUniqueId) in
    	// "addContactUniqueId" is uniqueId of this request, that sends back to client as a callback
    	// do whatever you want with this unique Id
    
    }, completion: { (myResponse) in
    	// this response is of type "ContactModel" but you have to froce cast it as below
    	let myResponseModel: ContactModel = addContactResponse as! ContactModel
    })


**۴- updateContact:**

آپدیت کردن اطلاعات مخاطب.

مشخصات جدید کاربر را به همرا id (همان آیدی مخاطب که پس از ذخیره ، یا به هنگام استفاده از سرویس لیست مخاطبین دریافت کرده اید) در لیست پارامتر ورودی به این متد بدهید تا عملیات تغییر مشخصات مخاطب مورد نظر صورت گیرد. پاسخ مشابه سرویس قبلی (AddContact) خواهد بود.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس UpdateContactsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد updateContacts .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی هم، جواب درخواست ساخت مخاطب جدید را بصورت مدل ContactModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of updateContact request:
    
    // this is the model that you have to create to pass it through the "updateContacts" method
    let inputModel = UpdateContactsRequestModel(cellphoneNumber:  "0935****233",    //
                                                email:            "mehyar@me.com",  //
                                                firstName:        "Sina",           //
                                                id:               10,               //
                                                lastName:         "Rokni",          //
                                                uniqueId:         nil)              //
    
    Chat.sharedInstance.updateContact(updateContactsInput: inputModel, uniqueId: { (updateContactUniqueId) in
    	// "updateContactUniqueId" is uniqueId of this request, that sends back to client as a callback
    	// do whatever you want with this unique Id
    
    }, completion: { (updateContactResponse) in
    	// this response is of type "ContactModel" but you have to froce cast it as below
    	let myResponseModel: ContactModel = updateContactResponse as! ContactModel
    })


**۵- removeContact:** 

حذف کردن یک مخاطب.

با دریافت آیدی مخاطب، آن مخاطب را حذف می‌کند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس RemoveContactsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد removeContact .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی هم پاسخ درخواست پاک کردن مخاطب را بصورت مدل RemoveContactModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of removeContact request:
    
    // this is the model that you have to create to pass it through the "removeContacts" method
    let inputModel = RemoveContactsRequestModel(id:        4121,  // id of your contact that you want to remove it
                                                uniqueId:  nil)   // 
    
    Chat.sharedInstance.removeContact(removeContactsInput: inputModel, uniqueId: { (removeContactUniqueId) in
    	// "removeContactUniqueId" is uniqueId of this request, that sends back to client as a callback
    	// do whatever you want with this unique Id
    
    }, completion: { (removeContactResponse) in
    	// this response is of type "RemoveContactModel" but you have to froce cast it as below
    	let myResponseModel: RemoveContactModel = removeContactResponse as! RemoveContactModel
    })


**۶-block:**

بلاک کردن یک مخاطب یا یک ترد.

با دریافت آیدی مخاطب(contactId)، آیدی یوزر(userId) یا تردآیدی(threadId) امکان ارتباط با او را مسدود میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس BlockContactsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد blockContact .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی هم پاسخ درخواست بلاک را بصورت مدل BlockedContactModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of blockContact request:
    
    // this is the model that you have to create to pass it through the "blockContacts" method
    let inputModel = BlockContactsRequestModel(contactId:  81,   //
                                               threadId:   nil,  //
                                               typeCode:   nil,  //
                                               userId:     nil,  //
                                               uniqueId:   nil)  //
    
    Chat.sharedInstance.blockContact(blockContactsInput: inputModel, uniqueId: { (blockContactUniqueId) in
    	// "blockContactUniqueId" is uniqueId of this request, that sends back to client as a callback
    	// do whatever you want with this unique Id
    
    }, completion: { (blockContactResponse) in
    	// this response is of type "BlockedContactModel" but you have to froce cast it as below
    	let myResponseModel: BlockedContactModel = blockContactResponse as! BlockedContactModel
    })``


**۷- getBlockContactList:**

لیست مخاطب های بلاک شده را باز میگرداند.

با پر کردن مقادیر ورودی count و offset میتوانید تنظیمات صفحه بندی را اعمال کنید.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس GetBlockedContactListRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد getBlockedContacts .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی هم  لیست مخاطب های بلاک شده را بصورت مدل GetBlockedContactListModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of getBlockedList request:
    
    // this is the model that you have to create to pass it through the "getBlockedContacts" method
    let inputModel = GetBlockedContactListRequestModel(count:     nil,   //
                                                       offset:    nil,   //
                                                       typeCode:  nil,   //
                                                       uniqueId:  nil)   //
    
    Chat.sharedInstance.getBlockedContacts(getBlockedContactsInput: inputModel, uniqueId: { (getBlockedContactListUniqueId) in
    	// "getBlockedContactListUniqueId" is uniqueId of this request, that sends back to client as a callback
    	// do whatever you want with this unique Id
    
    }, completion: { (bockedListResponse) in
    	// this response is of type "GetBlockedContactListModel" but you have to froce cast it as below
    	let myResponseModel: GetBlockedContactListModel = bockedListResponse as! GetBlockedContactListModel
    })


**۸-unblock:**

بیرون آوردن مخاطب

با دریافت بلاک آیدیblockId (آیدی مخاطب از لیست مسدود شده ها)، یا آیدی مخاطب(contactId)، یا آیدی یوزر(userId)، یا آیدی ترد(threadId) امکان ارتباط مجدد با مخاطب را برقرار میکند و مخاطب یا ترد، از لیست مسدود شده ها خارج میشود.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس UnblockContactsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد unblockContact .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی هم پاسخ درخواست آن-بلاک را بصورت مدل BlockedContactModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of unblock request:
    
    // this is the model that you have to create to pass it through the "unblockContact" method
    let inputModel = UnblockContactsRequestModel(blockId:   141,	//
                                                 contactId: nil,	//
                                                 threadId:  nil,	//
                                                 typeCode:  nil,	//
                                                 userId:    nil,	//
                                                 uniqueId:  nil)	//
    
    Chat.sharedInstance.unblockContact(unblockContactsInput: inputModel, uniqueId: { (unblockContactUniqueId) in
    	// "unblockContactUniqueId" is uniqueId of this request, that sends back to client as a callback
    	// do whatever you want with this unique Id
    
    }, completion: { (unblockResponse) in
    	// this response is of type "BlockedContactModel" but you have to froce cast it as below
    	let myResponseModel: BlockedContactModel = unblockResponse as! BlockedContactModel
    })


**۹- syncContact:** 

همگام سازی مخاطب ها.

تمامی مخاطبین دستگاه را که در لیست مخاطبین اپلیکیشن شما نیستند ، به آن اضافه میکند.

ورودی:

این متد پارامتر ورودی ندارد.

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی هم پاسخ درخواست آن را بصورت مدل ContactModel بازمیگرداند.

    // Request
    // an example of syncContact request:
    
    Chat.sharedInstance.syncContacts(uniqueId: { (syncContactUniqueId) in
    	// "syncContactUniqueId" is uniqueId of this request, that sends back to client as a callback
    	// do whatever you want with this unique Id
    
    }, completion: { (myResponse) in
    	// this response is of type "ContactModel" but you have to froce cast it as below
    	let myResponseModel: ContactModel = myResponse as! ContactModel
    })


**نکته:**

در تمامی متدهای ذکر شده در بالا، خروجی بصورت مدلی خواهد بود که شما میتوانید‌ از آن استفاده کنید.

همچنین می توانید با فراخوانی متد ()returnDataAsJSON ، خروجی را بصورت JSON مشاهده کنید.

بطور مثال:

    let myResponseJSON: JSON = myResponseModel.returnDataAsJSON()


_________________________________

-----------------------------------

در حال حاضر، برای ارسال پارامترهای ورودی به متدهای مورد نظر، به جز روشی که میتوانید با ساخت مدل مربوطه به هر درخواست، این کار را انجام دهید، روش دیگری نیز وجود دارد که میتوانید  یک فایل JSON را بعنوان پارامترهای ورودی مورد نظر خود به متد مربوطه پاس دهید.

نکته: در خروجی متدی که پارامترهای ورودی را بصورت JSON میدهید، خروجی Cache به شما برنمیگردد!

نکته: ترجیح بر این است که از حالت اول (ساختن مدل ورودی) استفاده کنید که در بالا بصورت جزء به جزء توضیح داده شده.

نکته: توجه داشته باشید که احتمالا در آینده ی نزدیک، استفاده از JSON برای پرکردن پارامترهای ورودی deprecate اعلام خواهد شد.



### مدیریت ترد ها

**۱- getThreads:**

لیست تمام ترد های اخیرا ایجاد شده ی کاربر را به ترتیب زمانی و بر اساس متغیر های صفحه بندی (count, offset) نشان خواهد داد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس GetThreadsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد getThreads .

خروجی:

در خروجی این متد، ۳ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، لیست تمامی تردهای موجود کاربر را بصورت مدل GetThreadsModel بازمیگرداند (با توجه به پارامترهای ارسالی).

سومی، جواب بلادرنگی است که کاربر درصورت فعال کردن گزینه ی استفاده از Cache، از دیتابیس داخلی خود دریافت میکند. (بعد از دریافت جواب سرور، این دیتابیس بصورت خودکار آپدیت میشود)

مثالی از فراخوانی این متد:

    // Request
    // an example of getThreads request:
    
    // this is the model that you have to create to pass it through the "getThreads" method
    let inputModel = GetThreadsRequestModel(count:                 9,    //
                                            creatorCoreUserId:     nil,  //
                                            metadataCriteria:      nil,  //
                                            name:                  nil,  //
                                            new:                   nil,  //
                                            offset:                0,    //
                                            partnerCoreContactId:  nil,  //
                                            partnerCoreUserId:     nil,  //
                                            threadIds:             nil,  //
                                            typeCode:              nil,  //
                                            uniqueId:              nil)  //
    
    Chat.sharedInstance.getThreads(getThreadsInput: inputModel, uniqueId: { (getThreadUniqueId) in
      // "getThreadUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (getThreadServerResponse) in
      // this response is of type "GetThreadsModel" but you have to froce cast it as below
      let myResponseModel: GetThreadsModel = getThreadServerResponse as! GetThreadsModel
    
    }, cacheResponse: { (getThreadCacheResponse) in
      // this it the cache response of this request
      // output of this response, is of type "GetThreadsModel". (there is no need to cast is as sth...)
    })


**۲- updateThreadInfo:**

با فراخوانی این متد میتوانید مشخصات یک ترد را تغییر دهید.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس UpdateThreadInfoRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد updateThreadInfo .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، جواب سرور به این ریکوئست را بصورت مدل GetThreadsModel برمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of updatrThreadInfo request:
    
    // this is the model that you have to create to pass it through the "createThread" method
    let inputModel = UpdateThreadInfoRequestModel(description:  nil,         //
                                                  image:        nil,         //
                                                  metadata:     nil,         //
                                                  threadId:     1113,        //
                                                  title:        "newTitle",  //
                                                  typeCode:     nil,         //
                                                  uniqueId:     nil)         //
    
    Chat.sharedInstance.updateThreadInfo(updateThreadInfoInput: inputModel, uniqueId: { (updateThreadInfoUniqueId) in
      // "updateThreadInfoUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (updateThreadResponse) in
      // this response is of type "GetThreadsModel" but you have to froce cast it as below
      let myResponseModel = updateThreadResponse as! GetThreadsModel
    })


**۳- createThread:**

ساخت یک ترد ، شامل ساخت ترد نفر به نفر (چت دو نفره) ، یا ترد جمعی (گروه) می باشد. در حالت عادی نحوه ی ایجاد هر دو مدل یکسان است ، تفاوت در تعداد نفرات گروه نسبت به ترد دو نفره میباشد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس CreateThreadRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد createThread .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی پاسخ سرور به درخواست کاربر را بصورت مدل CreateThreadModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of createThread request:
    
    // this is the model that you have to create to pass it through the "createThread" method
    let inviteeArray: [Invitee] = [Invitee(id:      "099****27",                                    //
                                           idType:  InviteeVOidTypes.TO_BE_USER_CELLPHONE_NUMBER)]  //
    
    let inputModel = CreateThreadRequestModel(description:  nil,                 //
                                              image:        nil,                 //
                                              invitees:     inviteeArray,        //
                                              metadata:     nil,                 // 
                                              title:        "New Group",         //
                                              type:         ThreadTypes.NORMAL,  //
                                              uniqueId:     nil)                 //
    
    Chat.sharedInstance.createThread(createThreadInput: inputModel, uniqueId: { (createThreadUniqeuId) in
      // "createThreadUniqeuId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (myCreateThreadResponse) in
      // this response is of type "CreateThreadModel" but you have to froce cast it as below
      let myResponseModel: CreateThreadModel = myCreateThreadResponse as! CreateThreadModel
    })


**۴- createThreadWithMessage:**

ساخت یک ترد ، شامل ساخت ترد نفر به نفر (چت دو نفره) ، یا ترد جمعی (گروه) وهمچنین ارسال همزمان مسیج می باشد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس CreateThreadWithMessageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد createThread .

خروجی:

در خروجی این متد، ۵ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، لیست تمامی مسیج های کاربر را بصورت مدل CreateThreadModel بازمیگرداند.

سومی، پیغام sent شدن مسیج میباشد (از نوع SendMessageModel) که از سمت سرور برمیگردد.

چهارمی، پیغام deliver شدن مسیج می باشد (از نوع SendMessageModel) که از سمت سرور برمیگردد.

پنجمی، پیغام seen شدن مسیج می باشد (از نوع SendMessageModel) که از سمت سرور برمیگردد.

مثالی از فراخوانی این متد:

    // Request
    // an example of creatThreadWithMessage request:
    
    // this is the model that you have to create to pass it through the "creatThreadWithMessage" method
    let inviteeArray: [Invitee] = [Invitee(id:      "099****27",                                    //
                                           idType:  InviteeVOidTypes.TO_BE_USER_CELLPHONE_NUMBER)]  //
    
    let inputModel = CreateThreadWithMessageRequestModel(threadDescription:           nil,                         //
                                                         threadImage:                 nil,                         //
                                                         threadInvitees:              inviteeArray,                //
                                                         threadMetadata:              nil,                         //
                                                         threadTitle:                 "title",                     //
                                                         threadType:                  ThreadTypes.NORMAL,          //
                                                         messageForwardedMessageIds:  nil,                         //
                                                         messageForwardedUniqueIds:   nil,                         //
                                                         messageMetaData:             nil,                         //
                                                         messageRepliedTo:            nil,                         //
                                                         messageSystemMetaData:       nil,                         //
                                                         messageText:                 "This is The Message Text",  //
                                                         messageType:                 nil,                         //
                                                         uniqueId:                    nil)                         //
    
    Chat.sharedInstance.creatThreadWithMessage(creatThreadWithMessageInput: inputModel, uniqueId: { (createWithSendMessageUniqeuId) in
      // "createThreadUniqeuId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (createThreadResponse) in
      // this response is of type "CreateThreadModel" but you have to froce cast it as below
      let myResponseModel: CreateThreadModel = createThreadResponse as! CreateThreadModel
    
    }, onSent: { (isSent) in
      // when the message sends successfully, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let sentModel: SendMessageModel = isSent as! SendMessageModel
    
    }, onDelivere: { (isDeliver) in
      // when the message is delivered, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let deliverModel: SendMessageModel = isDeliver as! SendMessageModel
    
    }, onSeen: { (isSeen) in
      // when the message is seen, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let seenModel: SendMessageModel = isSeen as! SendMessageModel
    })


**۵- leaveThread:**

با دریافت آیدی ترد ، کاربر را از ترد مربوطه خارج میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس LeaveThreadRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد leaveThread .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، نتیجه ترک ترد را بصورت مدل CreateThreadModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of leaveThread request:
    
    // this is the model that you have to create to pass it through the "leaveThread" method
    let inputModel = LeaveThreadRequestModel(content:   nil,   //
                                             threadId:  1343,  //
                                             typeCode:  nil,   //
                                             uniqueId:  nil)   //
    
    Chat.sharedInstance.leaveThread(leaveThreadInput: inputModel, uniqueId: { (leaveThreadUniqueId) in
    	// "leaveThreadUniqueId" is uniqueId of this request, that sends back to client as a callback
    	// do whatever you want with this unique Id
    
    }, completion: { (leaveThreadResponse) in
    	// this response is of type "CreateThreadModel" but you have to froce cast it as below
    	let myResponseModel: CreateThreadModel = leaveThreadResponse as! CreateThreadModel
    })


**۶- spamPvThread:**

با دریافت آیدی مربوط به یک ترد ، آن ترد را اسپم میکنم.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس SpamPvThreadRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد spamPvThread .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، جواب سرور به این ریکوئست را ۳ بار بصورت زیر برمیگرداند:

 ThreadModel (بابت ترک ترد)، ‌BlockModel (بابت بلاک کردن ترد)، ClearHistoryModel (بابت پاک کردن چت‌های داخل ترد) 

مثالی از فراخوانی این متد:

    // Request
    // an example of spamPvThread request:
    
    // this is the model that you have to create to pass it through the "spamPvThread" method
    let inputModel = SpamPvThreadRequestModel(threadId:  2,    //
                                              typeCode:  nil,  //
                                              uniqueId:  nil)  //
    
    Chat.sharedInstance.spamPvThread(spamPvThreadInput: inputModel, uniqueId: { (spamPvThreadUniqueId) in
      // "spamPvThreadUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (spamThreadResponse) in
    
      // this response is of type "ThreadModel" that you have to froce cast it as below
      if let leaveThreadResponse = spamThreadServerResponseModel as? ThreadModel {
        self.responseCallback?(leaveThreadResponse)
    
      // this response is of type "BlockedContactModel" that you have to froce cast it as below
      } else if let blockThreadResponse = spamThreadServerResponseModel as? BlockedContactModel  {
        self.responseCallback?(blockThreadResponse)
    
      // this response is of type "ClearHistoryModel" that you have to froce cast it as below
      } else if let clearHistoryResponse = spamThreadServerResponseModel as? ClearHistoryModel {
        self.responseCallback?(clearHistoryResponse)
      }
    
    })


**۷- muteThread:**

با دریافت آیدی ترد ، ترد مربوطه را mute میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس MuteAndUnmuteThreadRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد muteThread .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، جواب سرور به این ریکوئست را بصورت مدل MuteUnmuteThreadModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of muteThread request:
    
    // this is the model that you have to create to pass it through the "muteThread" method
    let inputModel = MuteAndUnmuteThreadRequestModel(subjectId:  1101,  //
                                                     typeCode:   nil,   //
                                                     uniqueId:   nil)   //
    
    Chat.sharedInstance.muteThread(muteThreadInput: inputModel, uniqueId: { (muteThreadUniqueId) in
      // "muteThreadUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (muteThreadResponse) in
      // this response is of type "MuteUnmuteThreadModel" but you have to froce cast it as below
      let myResponseModel: MuteUnmuteThreadModel = muteThreadResponse as! MuteUnmuteThreadModel
    })


**۸- unmuteThread:**

با دریافت آیدی ترد  ، مشخصه ی mute ترد مربوطه را در صورت فعال بودن ، غیرفعال میکند.

_ورودی:_

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس MuteAndUnmuteThreadRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد unmuteThread .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، جواب سرور به این ریکوئست را بصورت مدل MuteUnmuteThreadModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of unmuteThread request:
    
    // this is the model that you have to create to pass it through the "unmuteThread" method
    let inputModel = MuteAndUnmuteThreadRequestModel(subjectId: 1101,   //
                                                     typeCode:   nil,   //
                                                     uniqueId:   nil)   //
    
    Chat.sharedInstance.unmuteThread(unmuteThreadInput: inputModel, uniqueId: { (unmuteThreadUniqueId) in
      // "unmuteThreadUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (unmuteThreadResponse) in
      // this response is of type "MuteUnmuteThreadModel" but you have to froce cast it as below
      let myResponseModel: MuteUnmuteThreadModel = unmuteThreadResponse as! MuteUnmuteThreadModel
    })


**۹- getThreadParticipants:**

اعضای یک ترد با توجه به پارامترهای ورودی، نشان میدهد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس GetThreadParticipantsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد getThreadParticipants .

خروجی:

در خروجی این متد، ۳ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، لیست تمامی اعضای یک ترد را بصورت مدل GetThreadParticipantsModel بازمیگرداند.

سومی، جواب بلادرنگی است که کاربر درصورت فعال کردن گزینه ی استفاده از Cache، از دیتابیس داخلی خود دریافت میکند. (بعد از دریافت جواب سرور، این دیتابیس بصورت خودکار آپدیت میشود)

مثالی از فراخوانی این متد:


    // Request
    // an example of getThreadParticipants request:
    
    // this is the model that you have to create to pass it through the "getThreadParticipants" method
    let inputModel = GetThreadParticipantsRequestModel(admin:           nil,   //
                                                       count:           5,     //
                                                       firstMessageId:  nil,   //
                                                       lastMessageId:   nil,   //
                                                       name:            nil,   //
                                                       offset:          0,     //
                                                       threadId:        1330,  //
                                                       typeCode:        nil,   //
                                                       uniqueId:        nil)   //
    
    Chat.sharedInstance.getThreadParticipants(getThreadParticipantsInput: inputModel, uniqueId: { (getThreadParticipantUniqueId) in
      // "getThreadParticipantUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (threadParticipantsServerResponse) in
      // this response is of type "GetThreadParticipantsModel" but you have to froce cast it as below
      let myResponseModel: GetThreadParticipantsModel = threadParticipantsServerResponse as! GetThreadParticipantsModel
    
    }, cacheResponse: { (threadParticipantsCacheResponse) in
      // this it the cache response of this request
      // output of this response, is of type "GetThreadParticipantsModel". (there is no need to cast is as sth...)
    })


**۱۰- addParticipants:**

با دریافت آیدی ترد و لیستی از از آیدی مخاطبین (contact Id) ، آنها را به اعضای ترد مربوطه اضافه میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس AddParticipantsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد addParticipants .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، نتیجه ی اضافه کردن عضو به ترد را بصورت مدل AddParticipantModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of addParticipants request:
    
    // this is the model that you have to create to pass it through the "addParticipants" method
    let inputModel = AddParticipantsRequestModel(contacts:  [2202, 952, 1281, 2306],  //
                                                 threadId:  1330,                     //
                                                 typeCode:  nil,                      //
                                                 uniqueId:  nil)                      //
    
    Chat.sharedInstance.addParticipants(addParticipantsInput: inputModel, uniqueId: { (addParticipantsUniqueId) in
      // "addParticipantsUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (addParticipantsResponse) in
      // this response is of type "AddParticipantModel" but you have to froce cast it as below
      let response: AddParticipantModel = addParticipantsResponse as! AddParticipantModel
    })


**۱۱- removeParticipants:**

با دریافت آیدی ترد و لیستی از آیدی کاربران (userId)، آنها را از ترد مورد نظر حذف میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس RemoveParticipantsRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد removeParticipants .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، نتیجه ی حذف کردن عضو از ترد را بصورت مدل RemoveParticipantModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of removeParticipants request:
    
    // this is the model that you have to create to pass it through the "removeParticipants" method
    let inputModel = RemoveParticipantsRequestModel(contacts:  [1],   //
                                                    threadId:  1330,  //
                                                    typeCode:  nil,   //
                                                    uniqueId:  nil)   //
    
    Chat.sharedInstance.removeParticipants(removeParticipantsInput: inputModel, uniqueId: { (removeParticipantsUniqueId) in
      // "removeParticipantsUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (removeParticipantsResponse) in
      // this response is of type "RemoveParticipantModel" but you have to froce cast it as below
      let response: RemoveParticipantModel = removeParticipantsResponse as! RemoveParticipantModel
    })


**۱۲- setRole:**

با دریافت آیدی ترد و همچنین آیدی یوزر، میتواند به یوزر رول های ادمین بدهد (یا برعکس، رول‌های ادمین را از یوزر بگیرد)

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساخت و ارسال آرایه‌ای از کلاس SetRoleRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد setRole .

خروجی:

در خروجی این متد، ۳ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، جواب سرور به این ریکوئست را بصورت مدل UserRolesModel بازمیگرداند.

سومی، جواب بلادرنگی است که کاربر درصورت فعال کردن گزینه ی استفاده از Cache، از دیتابیس داخلی خود دریافت میکند. (بعد از دریافت جواب سرور، این دیتابیس بصورت خودکار آپدیت میشود)

مثالی از فراخوانی این متد:

    // Request
    // an example of setRole request:
    
    // this is the model that you have to create to pass it through the "setRole" method
    let inputModel = SetRoleRequestModel(roles:           [Roles.CHANGE_THREAD_INFO, Roles.EDIT_MESSAGE_OF_OTHERS],  //
                                         roleOperation:   RoleOperations.Add,  //
                                         threadId:        1330,                //
                                         typeCode:        nil,                 //
                                         uniqueId:        nil,                 //
                                         userId:          2244)                //
    
    Chat.sharedInstance.setRole(setRoleInput: [inputModel], uniqueId: { (setRoleUniqueId) in
      // "setRoleUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (setRoleServerResponse) in
      // this response is of type "UserRolesModel" but you have to froce cast it as below
      let myResponseModel = setRoleServerResponse as! UserRolesModel
    
    }, cacheResponse: { (setRoleCacheResponse) in
      // this it the cache response of this request
      // output of this response is of type "UserRolesModel". (there is no need to cast is as sth...)
    })


**۱۳- getHistory:**

با دریافت آیدی مربوط به یک ترد ، تاریخچه ی آن را بر اساس تنظیمات صفحه بندی (count,offset) نشان خواهد داد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس GetHistoryRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد getHistory .

خروجی:

در خروجی این متد، ۹ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، لیست تمامی مسیج های کاربر را بصورت مدل GetHistoryModel بازمیگرداند (با توجه به پارامترهای ارسالی).

سومی، جواب بلادرنگی است که کاربر درصورت فعال کردن گزینه ی استفاده از Cache، از دیتابیس داخلی خود دریافت میکند. (بعد از دریافت جواب سرور، این دیتابیس بصورت خودکار آپدیت میشود)

چهارمی، مسیج‌های متنی ارسالی که هنوز جوابشون از سمت سرور نیومده رو برمیگردونه.

پنجمی، مسیج‌های edit شده‌ی ارسالی که هنوز جوابشون از سمت سرور نیومده رو برمیگردونه.

ششمی، مسیج‌های forward شده‌ی ارسالی که هنوز جوابشون از سمت سرور نیومده رو برمیگردونه.

هفتمی، مسیج‌های همراه با ارسال فایل که هنوز جوابشون از سمت سرور نیومده یا هنوز آپلودشون کامل نشده رو برمیگردونه.

هشتمی، مسیج‌های آپلود عکس که هنوز جوابشون از سمت سرور نیومده یا هنوز آپلودشون کامل نشده رو برمیگردونه.

نهمی، مسیج‌های آپلود فایل که هنوز جوابشون از سمت سرور نیومده یا هنوز آپلودشون کامل نشده رو برمیگردونه.

مثالی از فراخوانی این متد:

    // Request
    // an example of getHistory request:
    
    // this is the model that you have to create to pass it through the "getHistory" method
    let inputModel = GetHistoryRequestModel(count:               2,    //
                                            firstMessageId:      nil,  //
                                            fromTime:            nil,  //
                                            lastMessageId:       nil,  //
                                            messageId:           nil,  //
                                            metadataCriteria:    nil,  //
                                            offset:              nil,  //
                                            order:               nil,  //
                                            query:               nil,  //
                                            threadId:            128,  //
                                            toTime:              nil,  //
                                            typeCode:            nil,  //
                                            uniqueId:            nil)  //
    
    Chat.sharedInstance.getHistory(getHistoryInput: inputModel, uniqueId: { (getHistoryUniqueId) in
      // "getHistoryUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (getHistoryServerResponse) in
      // this response is of type "GetHistoryModel" but you have to froce cast it as below
      let myResponseModel: GetHistoryModel = getHistoryServerResponse as! GetHistoryModel
    
    }, cacheResponse: { (getHistoryCacheResponse) in
      // this it the cache response of this request
      // output of this response, is of type "GetHistoryModel". (there is no need to cast is as sth...)
    
    }, textMessagesNotSent: { ([QueueOfWaitTextMessagesModel]) in
      // this response contain all messages that has not sent yet!
      // you have to cast it as [QueueOfWaitTextMessagesModel]
    
    }, editMessagesNotSent: { ([QueueOfWaitEditMessagesModel]) in
      // this response contain all edite messages that has not sent yet!
      // you have to cast it as [QueueOfWaitEditMessagesModel]
    
    }, forwardMessagesNotSent: { ([QueueOfWaitForwardMessagesModel]) in
      // this response contain all forward messages that has not sent yet!
      // you have to cast it as [QueueOfWaitForwardMessagesModel]
    
    }, fileMessagesNotSent: { ([QueueOfWaitFileMessagesModel]) in
      // this response contain all file messages that has not sent yet!
      // you have to cast it as [QueueOfWaitFileMessagesModel]
    
    }, uploadImageNotSent: { ([QueueOfWaitUploadImagesModel]) in
      // this response contain all uploadImage requests that has not sent yet!
      // you have to cast it as [QueueOfWaitUploadImagesModel]
    
    }, uploadFileNotSent: { ([QueueOfWaitUploadFilesModel]) in
      // this response contain all uploadFile requests that has not sent yet!
      // you have to cast it as [QueueOfWaitUploadFilesModel]
    })


**۱۴- clearHistory:**

با دریافت آیدی ترد ، تمامی مسیج های داخل ترد را پاک میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس ClearHistoryRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد clearHistory .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، جواب سرور به این ریکوئست را بصورت مدل ClearHistoryModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of clearHistory request:
    
    // this is the model that you have to create to pass it through the "getHistory" method
    let inputModel = ClearHistoryRequestModel(threadId:   1330,  //
                                              uniqueId:   nil)   //
    
    Chat.sharedInstance.clearHistory(clearHistoryInput: clearHistoryInput, uniqueId: { (clearHistoryUniqueId) in
      // "clearHistoryUniqueId" is uniqueId of this request, that sends back to client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (clearHistoryServerResponse) in
      // this response is of type "ClearHistoryModel" but you have to froce cast it as below
      let myResponseModel = clearHistoryServerResponse as! ClearHistoryModel
    })


**نکته:**

در تمامی متدهای ذکر شده در بالا، خروجی بصورت مدل خواهد بود که شما میتوانید از آن استفاده کنید.

همچنین می توانید با فراخوانی متد ()returnDataAsJSON ، خروجی را بصورت JSON مشاهده کنید.

بطور مثال:

```
let myResponseJSON: JSON = myResponseModel.returnDataAsJSON()
```




### مدیریت پیام ها

**۱- sendTextMessage:**

ارسال پیام به یک ترد، با دریافت آیدی ترد و پیغام ارسالی.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس SendTextMessageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد sendTextMessage .

خروجی:

در خروجی این متد، ۴ تا  completion handler داریم:

اولی: uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی: پس از ارسال پیغام، برای شما (send) را (از نوع SendMessageModel) برمیگرداند.

سومی: پس از دریافت پیغام،‌ توسط کاربر مقصد، برای شما (deliver) را (از نوع SendMessageModel) برمیگرداند.

چهارمی: پس از دیده شدن پیغام ارسالی توسط دیگر اعظای ترد،‌ب رای شما (seen) را (از نوع SendMessageModel) برمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of sendTextMessage request:
    
    // this is the model that you have to create to pass it through the "sendTextMessage" method
    let inputModel = SendTextMessageRequestModel(content:         "text message",  //
                                                 metaData:        metadata,        //
                                                 repliedTo:       nil,             //
                                                 systemMetadata:  nil,             //
                                                 threadId:        1328,            //
                                                 typeCode:        nil,             //
                                                 uniqueId:        nil)             //
    
    Chat.sharedInstance.sendTextMessage(sendTextMessageInput: inputModel, uniqueId: { (sendTextMessageUniqueId) in
      // "sendTextMessageUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, onSent: { (isSent) in
      // when the message sends successfully, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let sentModel: SendMessageModel = isSent as! SendMessageModel
    
    }, onDelivere: { (isDeliver) in
      // when the message is delivered, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let deliverModel: SendMessageModel = isDeliver as! SendMessageModel
    
    }, onSeen: { (isSeen) in
      // when the message is seen, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let seenModel: SendMessageModel = isSeen as! SendMessageModel
    })


**۲- editMessage:**

با دریافت آیدی پیام و محتوای جدید ، پیغام مربوطه را ویرایش میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس EditTextMessageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد editMessage .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، پاسخ این درخواست را از نوع EditMessageModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of editMessage request:
    
    // this is the model that you have to create to pass it through the "editMessage" method
    let inputModel = EditTextMessageRequestModel(content:         "text message",  //
                                                 metaData:        nil,             //
                                                 repliedTo:       nil,             //
                                                 subjectId:       10799,           //
                                                 typeCode:        nil,             //
                                                 uniqueId:        nil)             //
    
    Chat.sharedInstance.editMessage(editMessageInput: inputModel, uniqueId: { (editMessageUniqueId) in
      // "editMessageUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (editMessageResponse) in
      // this response is of type "EditMessageModel" but you have to froce cast it as below
      let myResponseModel = editMessageResponse as! EditMessageModel
    })


**۳- replyMessage:**

با دریافت آیدی ترد ، آیدی پیام ، و محتوای دلخواه ، پیام مورد نظر شما را انتخاب و محتوا را در پاسخ به آن پیام ارسال میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس ReplyTextMessageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد replyMessage .

خروجی:

با توجه به اینکه جنس این متد همانند sendTextMessage از نوع ارسال پیام است ، در نتیجه جهت عملیات پس از ارسال، دریافت، و دیده شدن پیام لازم خواهد داشت.

درنتیجه خروجی این متد، مشابه sendTextMessage خواهد بود.

مثالی از فراخوانی این متد:

    // Request
    // an example of replyMessage request:
    
    // this is the model that you have to create to pass it through the "replyMessage" method
    let inputModel = ReplyTextMessageRequestModel(content:      "text message",  //
                                                 metaData:      nil,             //
                                                 repliedTo:     15397,           //
                                                 subjectId:     1133,            //
                                                 typeCode:      nil,             //
                                                 uniqueId:      nil)             //
    
    Chat.sharedInstance.replyMessage(replyMessageInput: inputModel, uniqueId: { (replyMessageUniqueId) in
    	// "replyMessageUniqueId" is uniqueId of this request, that sends back to the client as a callback
    	// do whatever you want with this unique Id
    
    }, onSent: { (isSent) in
      // when the message sends successfully, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let sentModel: SendMessageModel = isSent as! SendMessageModel
    
    }, onDelivere: { (isDeliver) in
      // when the message is delivered, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let deliverModel: SendMessageModel = isDeliver as! SendMessageModel
    
    }, onSeen: { (isSeen) in
      // when the message is seen, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let seenModel: SendMessageModel = isSeen as! SendMessageModel
    })


**۴- forwardMessage:**

این متد ، باز ارسال یک یا چند پیام انتخابی را به یک ترد مشخص، با استفاده از آیدی پیام (جهت انتخاب آن) و آیدی ترد مقصد انجام خواهد داد. نوع این متد نیز ارسال پیام است.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس ForwardMessageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد forwardMessage .

خروجی:

با توجه به اینکه جنس این متد همانند sendTextMessage از نوع ارسال پیام است ، در نتیجه جهت عملیات پس از ارسال، دریافت، و دیده شدن پیام لازم خواهد داشت.

درنتیجه خروجی این متد، مشابه sendTextMessage خواهد بود.

مثالی از فراخوانی این متد:

    // Request
    // an example of forwardMessage request:
    
    // this is the model that you have to create to pass it through the "forwardMessage" method
    let inputModel = ForwardMessageRequestModel(messageIds:    [15395],   //
                                                metaData:      nil,       //
                                                repliedTo:     nil,       //
                                                subjectId:     1133,      //
                                                typeCode:      nil)       //
    
    Chat.sharedInstance.forwardMessage(forwardMessageInput: inputModel, uniqueIds: { (uniqueIdArr) in
      // "uniqueIdArr" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, onSent: { (isSent) in
      // when the message sends successfully, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let sentModel: SendMessageModel = isSent as! SendMessageModel
    
    }, onDelivere: { (isDeliver) in
      // when the message is delivered, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let deliverModel: SendMessageModel = isDeliver as! SendMessageModel
    
    }, onSeen: { (isSeen) in
      // when the message is seen, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let seenModel: SendMessageModel = isSeen as! SendMessageModel
    })


**۵- sendFileMessage:**

ارسال پیام با محتوای فایل به یک ترد مشخص. با دریافت آیدی ترد مقصد، آدرس فایل مورد نظر، محتوای متن همراه عکس و محتوای مورد نظر متادیتا، فایل ارسالی را پس از آپلود بر روی سرور، به همراه پیام ارسالی به ترد مقصد ارسال میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس SendFileMessageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد sendFileMessage .

خروجی:

با توجه به اینکه جنس این متد همانند sendTextMessage از نوع ارسال پیام است ، در نتیجه جهت عملیات پس از ارسال، دریافت، و دیده شدن پیام لازم خواهد داشت.

خروجی این متد، مشابه sendTextMessage خواهد بود، البته با یک completion handler دیگه، که درصد پیشرفت آپلود فایل در سرور را، بصورت عددی از نوع Double بین ۰ و ۱ نشان خواهد داد.

مثالی از فراخوانی این متد:

    // Request
    // an example of sendFileMessage request:
    
    // this is the model that you have to create to pass it through the "sendFileMessage" method
    let inputModel = SendFileMessageRequestModel(fileName:        "newPic",          //
                                                 imageName:       nil,               //
                                                 xC:              nil,               //
                                                 yC:              nil,               //
                                                 hC:              nil,               //
                                                 wC:              nil,               //
                                                 threadId:         1101,              //
                                                 content:         "empty message",   //
                                                 metaData:        nil,               //
                                                 repliedTo:       nil,               //
                                                 subjectId:      1101,              //
                                                 typeCode:        nil,               //
                                                 fileToSend:      data,              //
                                                 imageToSend:     nil)               //
    
    Chat.sharedInstance.sendFileMessage(sendFileMessageInput: inputModel, uniqueId: { (sendFileMessageUniqueId) in
      // "sendFileMessageUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, uploadProgress: { (progress) in
      // this is a Double between 0 and 1, that respresent the upload progress
    
    }, onSent: { (isSent) in
      // when the message sends successfully, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let sentModel: SendMessageModel = isSent as! SendMessageModel
    
    }, onDelivere: { (isDeliver) in
      // when the message is delivered, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let deliverModel: SendMessageModel = isDeliver as! SendMessageModel
    
    }, onSeen: { (isSeen) in
      // when the message is seen, this response of type "SendMessageModel" comes that you have to froce cast it as below
      let seenModel: SendMessageModel = isSeen as! SendMessageModel
    })


**۶- replyFileMessage:**

ارسال پیام با محتوای فایل در پاسخ به یک پیام مشخص.

با دریافت آیدی ترد مقصد و همچنین ایدی پیام، آدرس فایل مورد نظر، محتوای متن همراه عکس و محتوای مورد نظر متادیتا، فایل ارسالی را پس از آپلود بر روی سرور، به همراه پیام ارسالی به ترد مقصد ارسال میکند.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس SendFileMessageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد sendFileMessage .

خروجی:

با توجه به اینکه جنس این متد همانند sendTextMessage از نوع ارسال پیام است ، در نتیجه جهت عملیات پس از ارسال، دریافت، و دیده شدن پیام لازم خواهد داشت.

خروجی این متد، مشابه sendTextMessage خواهد بود، البته با یک completion handler دیگه، که درصد پیشرفت آپلود فایل در سرور را، بصورت عددی از نوع Double بین ۰ و ۱ نشان خواهد داد.

نحوه‌ی فراخوانی و پاسخ این متد، کاملا مشابه متد قبلی (SendFileMessage) می‌باشد.


**۷- deleteMessage:**

با دریافت آیدی پیام (messageId) ، پیام مربوطه را حذف خواهد کرد.

نکته: در صورتی که متغیر deleteForAll را با مقدار true پر کنید ، پیام مذکور از تاریخچه ی ترد همه ی اعضای آن ترد پاک خواهد شد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس DeleteMessageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد deleteMessage .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، پاسخ این درخواست را از نوع DeleteMessageModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of deleteMessage request:
    
    // this is the model that you have to create to pass it through the "deleteMessage" method
    let inputModel = DeleteMessageRequestModel(deleteForAll:    nil,    //
                                               subjectId:       10799,  //
                                               typeCode:        nil,    //
                                               uniqueId:        nil)    //
    
    Chat.sharedInstance.deleteMessage(deleteMessageInput: inputModel, uniqueId: { (deleteMEssageUniqueId) in
      // "deleteMEssageUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (deleteMessageResponse) in
      // this response is of type "DeleteMessageModel" but you have to froce cast it as below
      let myResponseModel = deleteMessageResponse as! DeleteMessageModel
    })


**۸- deleteMultipleMessages:**

با دریافت آیدی چند پیام (messageIds) ، پیام های مربوطه را حذف خواهد کرد.

نکته: در صورتی که متغیر deleteForAll را با مقدار true پر کنید ، پیام مذکور از تاریخچه ی ترد همه ی اعضای آن ترد پاک خواهد شد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس DeleteMultipleMessagesRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد deleteMultipleMessages .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، پاسخ این درخواست را از نوع DeleteMessageModel بازمیگرداند.

تنها تفاوت این متد با متد قبلی (deleteMessages) در این است که در پارامترهایی ورودی،‌ یک آرایه مسیج‌آیدی و یوینیک آیدی میگیرد.


**۹- cancelMessage:**

با استفاده از از این متد میتوانید پیام‌هایی که ارسال کردید اما هنوز ارسال نشده اند (پیام‌هایی که داخل صف قرار میگیرند و میتوانید اون‌ها رو با فراخوانی متد getHistory ببینید) رو کنسل کنید.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس CancelMessageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد cancelSendMessage .

خروجی:

در خروجی این متد، یک completion handler داریم:

اگر این ریکوئست را در صف پیام‌های ارسال نشده پیدا کند، آن پیام را از صف پاک کرده و مقدار true را برمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of cancelMessage request:
    
    // this is the model that you have to create to pass it through the "cancelSendMessage" method
    let inputModel = CancelMessageRequestModel(textMessageUniqueId:       "xxxyyyyyyzzzzzzzzz",  //
                                               editMessageUniqueId:       nil,                   //
                                               forwardMessageUniqueId:    nil,                   //
                                               fileMessageUniqueId:       nil,                   //
                                               uploadImageUniqueId:       nil,                   //
                                               uploadFileUniqueId:        nil)                   //
    
    Chat.sharedInstance.cancelSendMessage(cancelMessageInput: inputModel, completion: { (isSuccessfull) in
      // this response is of type "Boolean"
    })


**۱۰- messageDeliveryList:**

با فراخوانی این متد، میتوانید لیست افرادی که پیام شما به آن‌ها رسیده را ببینید.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس MessageDeliverySeenListRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد messageDeliveryList .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، پاسخ این درخواست را از نوع GetThreadParticipantsModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of messageDeliveryList request:
    
    // this is the model that you have to create to pass it through the "messageDeliveryList" method
    let inputModel = MessageDeliverySeenListRequestModel(count:       40,      //
                                                         messageId:   134453,  //
                                                         offset:      0,       //
                                                         typeCode:    nil,     //
                                                         uniqueId:    nil)     //
    
    Chat.sharedInstance.messageDeliveryList(messageDeliveryListInput: inputModel, uniqueId: { (deliveryListUniqueId) in
      // "deliveryListUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (deliverListResponse) in
      // this response is of type "GetThreadParticipantsModel" but you have to froce cast it as below
      let myResponseModel = deliverListResponse as! GetThreadParticipantsModel
    })

خروجی این متد همانند خروجی متد getThreadParticipant است.


**۱۱- messageSeenList:**

با فراخوانی این متد، میتوانید لیست افرادی که پیام شما را خوانده اند را ببینید.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس MessageDeliverySeenListRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد messageSeenList .

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی، uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی، پاسخ این درخواست را از نوع GetThreadParticipantsModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of messageSeenList request:
    
    // this is the model that you have to create to pass it through the "messageSeenList" method
    let inputModel = MessageDeliverySeenListRequestModel(count:       40,      //
                                                         messageId:   134453,  //
                                                         offset:      0,       //
                                                         typeCode:    nil,     //
                                                         uniqueId:    nil)     //
    
    Chat.sharedInstance.messageSeenList(messageSeenListInput: inputModel, uniqueId: { (seenListUniqueId) in
      // "seenListUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, completion: { (seenListResponse) in
      // this response is of type "GetThreadParticipantsModel" but you have to froce cast it as below
      let myResponseModel = seenListResponse as! GetThreadParticipantsModel
    })

خروجی این متد همانند خروجی متد getThreadParticipant است.


**۱۲- startTyping:**

هنگامی که کاربر شروع به تایپ کردن میکند، میتوانید با فراخوانی این متد، پیغام isTyping را واسه اعضای دیگر ترد بفرستید.

نکته: در نظر داشته باشید که حتما بعد از اینکه تایپ کردن کاربر به پایان رسید، متد stopTyping را فراخوانی کنید.

ورودی:

برای پر کردن پارامترهای ورودی این متد، فقط کافیست تردآیدی را بفرستید.

خروجی:

در خروجی این متد، یک completion handler داریم که درواقع uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

(برای فراخوانی متد stopTyping ، به این یونیک‌آیدی نیاز خواهید داشت)

مثالی از فراخوانی این متد:

    // Request
    // an example of startTyping request:
    
    Chat.sharedInstance.startTyping(threadId: 1244:, { (startTypingUniqueId) in
      // "startTypingUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // hold this uniqueId, because you'll need this id when calling the 'stopTyping'
    })


**۱۳- stopTyping:**

هنگامی که تایپ کردن کاربر به پایان رسید، این متد را فراخوانی کنید.

ورودی:

برای پر کردن پارامترهای ورودی این متد، فقط کافیست یونیک‌آیدی درخواست startTyping ای را که قبلا فرستادید را بفرستید.

خروجی:

این متد خروجی‌ای ندارد.

مثالی از فراخوانی این متد:

    // Request
    // an example of stopTyping request:
    
    Chat.sharedInstance.stopTyping(uniqueId: "zzzzzzyyyyyyxxxx)



### مدیریت فایل ها

**۱- uploadImage:** 

با دریافت فایل عکس، آن را بر روی سرور فایل ذخیره میکند.

در صورتی که میخواهید عکس را برش دهید ، مختصات شروع برش و طول و عرض برش را به عنوان ورودی به متد ارسال کنید.


ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس UploadImageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد uploadImage . 

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی: uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی: مقدار آپلود عکس را بصورت عددی بین ۰ تا ۱ (از نوع float) بازمیگرداند.سومی: جواب سرور به آپلود عکس را بصورت مدل UploadImageModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of uploadImage request:
    
    // this is the model that you have to create to pass it through the "uploadImage" method
    let inputModel = UploadImageRequestModel(dataToSend:        data,      //
                                             fileExtension:     nil,       //
                                             fileName:          "newPic",  //
                                             fileSize:          nil,       //
                                             originalFileName:  nil,       //
                                             threadId:          nil,       //
                                             uniqueId:          nil,       //
                                             xC:                nil,       //
                                             yC:                nil,       //
                                             hC:                nil,       //
                                             wC:                nil)       //
    
    Chat.sharedInstance.uploadImage(uploadImageInput: inputModel, uniqueId: { (UploadImageUniqueId) in
      // "UploadImageUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, progress: { (progress) in
      // this is a Double between 0 and 1, that represents the upload progress
    
    }, completion: { (response) in
      // this response is of type "UploadImageModel" but you have to force cast it as below
      let responseModel: UploadImageModel = response as! UploadImageModel
    })


**۲- uploadFile:**

با دریافت فایل، آن را در سرور فایل بارگذاری خواهد کرد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس UploadFileRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد uploadFile . 

خروجی:

در خروجی این متد، ۲ تا  completion handler داریم:

اولی: uniqueId این درخواست شما رو بصورت یک String برمیگرداند.

دومی: مقدار آپلود عکس را بصورت عددی بین ۰ تا ۱ (از نوع float) بازمیگرداند.

سومی: جواب سرور به آپلود عکس را بصورت مدل UploadFileModel بازمیگرداند.

مثالی از فراخوانی این متد:

    // Request
    // an example of uploadFile request:
    
    // this is the model that you have to create to pass it through the "uploadFile" method
    let inputModel = UploadFileRequestModel(dataToSend:        data,      //
                                            fileExtension:     nil,       //
                                            fileName:          "newPic",  //
                                            fileSize:          nil,       //
                                            originalFileName:  nil,       //
                                            threadId:          nil,       //
                                            uniqueId:          nil)       //
    
    myChatObject?.uploadFile(uploadFileInput: inputModel, uniqueId: { (uploadFileUniqueId) in
      // "uploadFileUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, progress: { (progress) in
      // this is a Double between 0 and 1, that represents the upload progress
    
    }, completion: { (response) in
      // this response is of type "UploadFileModel" but you have to force cast it as below
      let responseModel: UploadFileModel = response as! UploadFileModel
    })


**۳- getImage:**

با دریافت آیدی تصویر ذخیره شده و کد مشخصه ی آن (hashCode) لینک دریافت آن را در اختیار قرار میدهد.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس GetImageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد getImage . 

خروجی:

مثالی از فراخوانی این متد:

    // Request
    // an example of getImage request:
    
    // this is the model that you have to create to pass it through the "getImage" method
    let inputModel = GetImageRequestModel(actual:        nil,           //
                                          downloadable:  nil,           //
                                          height:        nil,           //
                                          hashCode:      "16632a16342-0.15843373456354997",  //
                                          imageId:       54404,         //
                                          width:         nil)           //
    
    Chat.sharedInstance.getImage(getImageInput: inputModel, uniqueId: { (getImageUniqueId) in
      // "getImageUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, progress: { (myDownloadProgress) in
      // this is a Double between 0 and 1, that respresents the download progress
    
    }, completion: { (data, responseModel) in
      // "data" is of kind Data, that represents the file itself
      // "response" is the UploadImageModel
    
    }, cacheResponse: { (cacheResponse, filePath) in
      // "cacheResponse" is the UploadFileModel
      // "filePath" is the address of the file in the local project Bundle
    })


**۴- getFile:**

با دریافت آیدی فایل ذخیره شده و کد مشخصه ی آن (hashCode) لینک آن را در اختیار قرار میدهد.این متد پارامتری به عنوان downloadable دارد که از نوع boolean است. در صورت مثبت بودن لینک فایل خروجی قابل دانلود خواهد بود.

ورودی:

برای پر کردن پارامترهای ورودی این متد، از روش زیر میتوانید این کار را انجام دهید:

ساختن یک مدل از کلاس GetImageRequestModel و پاس دادن آن بعنوان پارامتر ورودی به متد getImage . 

خروجی:

مثالی از فراخوانی این متد:

    // Request
    // an example of getImage request:
    
    // this is the model that you have to create to pass it through the "getImage" method
    let inputModel = GetFileRequestModel(downloadable:    true,    //
                                         fileId:          52171,   //
                                         hashCode:        "168232d744d-0.9990232707506134")   //
    
    Chat.sharedInstance.getFile(getFileInput: inputModel, uniqueId: { (getFileUniqueId) in
      // "getFileUniqueId" is uniqueId of this request, that sends back to the client as a callback
      // do whatever you want with this unique Id
    
    }, progress: { (myDownloadProgress) in
      // this is a Double between 0 and 1, that respresent the download progress
    
    }, completion: { (data, response) in
      // "data" is of kind Data, that represents the file itself
      // "response" is the UploadImageModel
    
    }, cacheResponse: { (cacheResponse, filePath) in
      // "cacheResponse" is the UploadFileModel
      // "filePath" is the address of the file in the local project Bundle
    })


**۵- manageUpload:**

با فراخوانی این متد میتوانید فایل‌ (یا عکسی) را که در حال آپلود می‌باشد مدیریت کنید. (suspend , resume, cancle)

ورودی:

برای مدیریت آپلود فایل، بعد از مشخص کردن اینکه این آپلود مربوط به عکس بوده یا فایل، کافیست یونیک‌آیدی ریکوئست upload را به همراه اکشنی که مد نظر دارید (suspend , resume, cancle) به این متد بفرستید.

خروجی:

در comletionHnadler این متد، پیغام مربوطه و اینکه آیا این درخواست موفقیت آمیز بوده یا خیر،‌ بصورت مقداری بولین برگشت داده خواهد شد.

مثالی از فراخوانی این متد:

    // Request
    // an example of manageUpload request:
    
    Chat.sharedInstance.manageUpload(image:         false,      //
                                     file:          true,       //
                                     withUniqueId:  "xxxxxxxyyyyyyyyzzzzzzz",    //
                                     withAction:    DownloaUploadAction.cancel,  //
                                     completion:    { (responseMessage, isSuccesfull) in
      // "responseMessage" is of type String
      // "isSuccesfull" is the Boolean
    })


**۶- manageDownload:**

با فراخوانی این متد میتوانید فایل‌ (یا عکسی) را که در حال دانلود می‌باشد مدیریت کنید. (suspend , resume, cancle)

ورودی:

برای مدیریت دانلود فایل، کافیست یونیک‌آیدی ریکوئست getFile را به همراه اکشنی که مد نظر دارید (suspend , resume, cancle) به این متد بفرستید.

خروجی:

در comletionHnadler این متد، پیغام مربوطه و اینکه آیا این درخواست موفقیت آمیز بوده یا خیر،‌ بصورت مقداری بولین برگشت داده خواهد شد.

مثالی از فراخوانی این متد:

    // Request
    // an example of manageDownload request:
    
    Chat.sharedInstance.manageDownload(withUniqueId:  "xxxxxxxyyyyyyyyzzzzzzz",    //
                                       withAction:    DownloaUploadAction.cancel,  //
                                       completion:    { (responseMessage, isSuccesfull) in
      // "responseMessage" is of type String
      // "isSuccesfull" is the Boolean
    })



### "Event Listeners"

با ساختن پکیج چت،‌ و همچنین تایید کردن ChatDelegate ، شما باید متدهای زیر را در کلاس خود، پیاده سازی کنید.این ها رویدادهایی هستند که از طریق پکیج چت اعلام میشوند.

رخداد تمامی رویداد ها با متدهای زیر قابل دریافت خواهند بود.

    func messageEvents(type: String, result: JSON) { }
    func threadEvents(type: String, result: JSON) { }
    func chatError(errorCode: Int, errorMessage: String, errorResult: Any?) { }
    func chatState(state: Int) { }
    func chatConnected() { }
    func chatReconnect() { }
    func chatThreadEvents() { }
    func chatReady() { }
    func chatDeliver(messageId: Int, ownerId: Int) { }


**۱- messageEvents:**

تمامی رویدادهایی که پس از فعل و انفعال پیام ها قابل رخداد است با این نام قابل دریافت است.

"message events" یا رویدادهای پیام دلایل مختلفی دارد، که به فراخور آن میتوانید عملیات مورد نظر خود را سمت اپلیکیشن انجام دهید.

این رویداد، ۲ مقدار به شما برمیگرداند؛ یکی تایپ و دیگری محتوای مربوطه

انواع تایپ های رویداد messageEvents عبارتند از:

, MESSAGE_NEW: با دریافت پیام جدید این رویداد رخ خواهد داد.
 ,MESSAGE_EDIT: ویرایش شدن یک پیغام در ترد، از طریق این رویداد به اعضای آن ترد اطلاع داده میشود.
 ,MESSAGE_DELIVERY: دریافت پیام توسط گیرنده توسط این رویداد به فرستنده اطلاع رسانی میشود.
, MESSAGE_SEEN: پس از دیده شدن پیغام توسط کاربر گیرنده ی پیام ، فرستنده توسط این رویداد از این امر مطلع میشود.

شما میتوانید با توجه به تایپ دریافتی، محتوای فرستاده شده در قسمت دوم را دریافت و عملیات متناسب را سمت اپلیکیشن خود انجام دهید.


**۲- threadEvents:**

تمامی رویداد های تردهایی که کاربر در آن عضو است یا به آن مرتبط می باشد از این طریق اعلام میشود.

رویدادهای مربوط به ترد ، انواع زیر را داراست که بسته به نوع آن می توانید عملیات متناسب را سمت اپلیکیشن خود انجام دهید:

, THREAD_NEW: ساخت ترد جدید را به اعضایی که در آن مشارکت خواهند داشت (Participants) اعلام میکند.
, THREAD_LAST_ACTIVITY_TIME: زمانی که فعل و انفعالی در یک ترد رخ دهد، زمان آخرین فعل و انفعال رخ داده به اعضای آن ترد اعلام خواهد شد.(اپلیکیشن جهت آپدیت لیست تردها بر اساس جدیدترین تغییرات آنها میتواند اقدام کند)
, THREAD_ADD_PARTICIPANTS: اضافه شدن فرد جدید به یک ترد را به همه ی اعضا اعلام میکند.
, THREAD_LEAVE_PARTICIPANTS: ترک کردن ترد توسط یک فرد را به اعضا اعلام میکند.
, THREAD_REMOVE_PARTICIPANTS: حذف شدن یک فرد از ترد را به اعضا اعلام میکند.
, THREAD_REMOVED_FROM: حذف شدن یک فرد از ترد را به او اعلام میکند.
, THREAD_RENAME: تغییر نام ترد توسط این رویداد به هر یک از اعضا اعلام میشود.
,THREAD_MUTE: پس از غیرفعال کردن نوتیفیکیشن یک ترد توسط کاربر به او اعلام میشود.
 ,THREAD_UNMUTE: پس از فعال کردن نوتیفیکیشن یک ترد توسط کاربر به او اعلام میشود.
, THREAD_INFO_UPDATED: در صورتی که اطلاعات داخل ترد نیاز به به روز رسانی داشته باشد (مثل زمانی که یک پیغام پاک میشود)، توسط این رویداد به دیگر اعضا اطلاع رسانی میشود.
 ,THREAD_UNREAD_COUNT_UPDATED: تعداد پیغام های خوانده نشده ی هر ترد توسط این رویداد به اعضای آن اعلام میشود.اپلیکیشن میتواند در لیست ترد های نمایش داده به کاربر ، تعداد پیغام های خوانده نشده ی هر کدام را اعلام کند.در صورتی که پیغام جدیدی به هر تردی اضافه شود ، تعداد پیغام های خوانده نشده ی آن آپدیت و بدین وسیله به کاربر (اعضای آن ترد) گزارش میشود.


**۳- chatError:**

تمامی خطا ها از سمت سرور توسط این رویداد به کاربر گزارش میشود.


**۴- chatState:**

تغییر وضعیت ارتباط با سرور پیام رسان را به کاربر اطلاع میدهد.

چهار وضعیت CONNECTED , CONNECTING , CLOSED , CLOSING قابل رخداد است.



### آدرس ها و تنظیمات

تنظیمات و آدرس های زیر (برای سرور سندباکس) ، باید به عنوان پارامتر ورودی در هنگام ساخت نمونه ی اولیه از پکیج داده شود.

    // SandBox Addresses:
    let socketAddress	= "wss://chat-sandbox.pod.land/ws"			// Socket Server Address
    let serverName		= "chat-server"						// Server to register on
    let ssoHost		= "https://accounts.pod.land"				// SSO Server Address
    let platformHost	= "https://sandbox.pod.land:8043/srv/basic-platform"	// Platform Core Server Address
    let fileServer		= "http://sandbox.fanapium.com:8080"			// File Server Address
    let token		= "b304d32ec4bd49d5992b90450a644d9e"			// SSO Token
    
    // create Chat object
    var myChatObject = Chat(socketAddress:		“Socket Address”,
                         ssoHost:			“SSO Host Address”,
                         platformHost:		”PlatForm Address”,
                         fileServer:		“File Server Address”,
                         serverName:		"chat-server",
                         token:			“TOKEN”,
                         msgPriority:		Int?,
                         msgTTL:			Int?,
                         httpRequestTimeout:	Int?,
                         actualTimingLog:		Bool?,
                         wsConnectionWaitTime:	Double,
                         connectionRetryInterval:	Int,
                         connectionCheckTimeout:	Int,
                         messageTtl:		Int,
                         reconnectOnClose:		Bool)

<div class="box-end">
</div>















