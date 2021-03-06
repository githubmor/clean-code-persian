# 9 تست های واحد

![unit tests](image-1-1.png "unit tests")

<div dir="rtl">

حرفه ما مسیر زیادی را در طی 10 سال گذشته پیموده است. در سال 1997 هیچکس در مورد توسعه آزمون محور چیزی نشنیده بود. برای اکثریت قریب به اتفاق ما ، تست های واحد چند خط کد بدرد نخور بودند که مطمئن شویم برنامه کار میکند. ما با زحمت کلاس ها و متد هایمان را مینوشتیم و بعد با چندین خط کد کثیف و از سرباز کنی، آن ها را تست می کردیم. معمولاً این حرکت شامل این میشود که یک برنامه درایور ساده را به پروژه اضافه کنیم، تا بتوانیم به صورت دستی کد را تست کنیم.

یادم میاد در اواسط دهه 90 داشتم یک برنامه با زبان ++C برای یک سیستم نهفته می نوشتم. برنامه یک تایمر ساده به شرح زیر بود:


`void Timer::ScheduleCommand(Command* theCommand, int milliseconds)`

الگوریتم کار ساده بود، متد execute از آبجکت command باید بعد از گذشت چند میلی ثانیه مشخص داخل یک ترد جدید فراخوانی می شد. اما مشکل اصلی این بود که چه طور باید این الگوریتم را تست کنیم.
برای انجام این کار خیلی سریع یک برنامه درایور صفحه کلید نوشتم. هر وقت که یک حرف تایپ می شد، برنامه فرمان چاپ را پنج ثانیه بعد صادر میکند. سپس یک شعر ریتمیک را تایپ کردم و منتظر ماندم تا شعر با پنج ثانیه تاخیر در صفحه چاپ شود.

"من ... یکی رو میخواستم ... فقط ... اون دختری که از ... دواج ... کرد ... با بابای ... عزیز... و پیرم"

در واقع من آن  شعر را در حالی که کلید "." را تایپ میکردم می خواندم. و بعد آن را دوباره هنگامی که نقطه ها چاپ شده بودند، خواندم.
این تست من شد! بعد از اینکه از کار کردن آن مطمئن شدم و آن را برای همکارانم توضیح دادم، کد تست را پاک کردم.
همینطور که قبلا گفتم، حرفه ما راه زیادی را طی کرده است. امروزه من برای تمام سوراخ و سنبه ها و گوشه های نرم افزار تست می نویسم تا مطمئن باشم همانطوری که من انتظار دارم کار می کند. من وابستگی کد را نسبت به سیستم عامل حذف میکنم، به جای آنکه بخواهم توابع مدیریت زمان مربوط به سیستم عامل را صدا بزنم. من برای کنترل کامل بر زمان، تمام توابع مدیریت زمان را به صورت جعلی می نویسم. من فرمان هایی که پرچم های وضعیت را تغییر می دهند، برنامه ریزی میکنم و بعد زمان را جلو می برم و پرچم ها را زیر نظر میگیرم که مقدارشان از false به true تغییر کند، آن هم درست زمانی که من مقدار زمان را تغییر دهم. 
وقتی که تمام تست ها پاس شدند، من مطمئن می شوم که اجرا کردن آن ها برای هر کسی که نیاز دارد با کد کار کند، راحت باشد. همینطور مطمئن می شوم که کد و تست با هم در یک پکیج حاضر شوند.
بله ما راه زیادی را طی کرده ایم. ، اما هنوز باید جلوتر برویم. روش چابک (Agile) و توسعه آزمون محور (TDD) خیلی از برنامه نویس ها را تشویق کرده که تست های واحد اتوماتیک بنویسند و همینطور به تعداد آن ها افزوده می شود. اما عجله زیاد برای افزودن تست، باعث شده که بسیاری از برنامه نویسان نکات مهم و حیاطی نوشتن تست خوب را جا بیندازند.

## سه قانون توسعه آزمون محور

تا الان همه می دانند که توسعه آزمون محور از ما میخواهد قبل از نوشتن کد نهایی (Production Code)، تست های واحد را بنویسیم. اما این قانون فقط قسمت کوچکی از توسعه آزمون محور است. این سه قانون را در نظر بگیرید:
<br />
**قانون اول** تنها زمانی شروع به نوشتن کد نهایی کنید که می خواهید یک تست شکست خورده را پاس کنید.
<br />
**قانون دوم** با شکست خوردن تست از نوشتن تست بعدی جلوگیری کنید.
<br />
**قانون سوم** تنها به مقداری کد نهایی بنویسید که برای پاس کردن تست شکست خورده کافی باشد.
<br />
این سه قانون شما را وارد یک چرخه ای می کند که شاید 30 ثانیه طول بکشد. تست ها و کد نهایی با هم نوشته می شوند، با این تفاوت که تست ها چند ثانیه از کد نهایی جلوتر هستند.
اگر ما به این روش کار کینم، ده ها تست به طور روزانه، صد ها تست ماهانه و هزاران تست در سال خواهیم نوشت. اگر به این روش کار کینم، این تست ها تمام کد های نهایی ما را پوشش می دهند. بخش عمده این تست ها که میتواند با اندازه کد نهایی رقابت کند، میتواند یک مشکل مدیریتی دلهره آور را ایجاد کند.

</div>