---
draft: false
aliases: ["/fa/"]
---

# کامیت‌های قراردادی 1.0.0

## خلاصه

استاندارد کامیت های قراردادی (Conventional Commits) یک روش ساده و سبک برای برای نوشتن پیام های کامیت هستند.
این روش مجموعه‌ای از قوانین مشخص را ارائه می‌دهد تا تاریخچه‌ی کامیت‌ها واضح‌تر و خواناتر باشد و همچنین امکان خودکارسازی ابزارهای مرتبط را فراهم می‌کند.  
این استاندارد با [SemVer (نسخه‌بندی معنایی)](http://semver.org) همخوانی دارد و تغییرات ایجاد شده در کامیت‌ها، از جمله ویژگی‌های جدید، اصلاحات و تغییرات اساسی را توصیف می‌کند.

ساختار پیام کامیت‌ها باید به این صورت باشد:

---

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```
---

<br />
این کامیت شامل عناصر ساختاری زیر است تا هدف تغییرات را به کاربران کتابخانه شما منتقل کند:

1. **fix:** کامیتی از _نوع_ `fix` که یک باگ را در کد برطرف می‌کند (این مورد با [`PATCH`](http://semver.org/#summary) در نسخه‌بندی معنایی مطابقت دارد).
2. **feat:** کامیتی از _نوع_ `feat` که یک قابلیت جدید به کد اضافه می‌کند (این مورد با [`MINOR`](http://semver.org/#summary) در نسخه‌بندی معنایی مطابقت دارد).
3. **BREAKING CHANGE:** کامیتی که شامل پاورقی (footer) `BREAKING CHANGE:` باشد یا علامت `!` را بعد از نوع (type) یا محدوده (scope) داشته باشد، نشان‌دهنده‌ی یک تغییر ناسازگار در API است (مطابق با [`MAJOR`](http://semver.org/#summary) در نسخه‌بندی معنایی).
یک BREAKING CHANGE می‌تواند بخشی از هر _نوع_ کامیتی باشد.
1. علاوه بر `fix:` و `feat:`، _انواع_ دیگری نیز مجاز هستند. به عنوان مثال، [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional) (بر اساس قوانین کامیت در [Angular convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)) استفاده از <span dir="ltr"> `build:`، `chore:`، `ci:`، `docs:`، `style:`، `refactor:`، `perf:`، `test:` </span> و موارد دیگر را توصیه می‌کند
2. پاورقی (footer) هایی غیر از <span dir="ltr"> `BREAKING CHANGE: <description>` </span> نیز می‌توانند استفاده شوند و از الگوی مشابه با [قالب استاندارد اطلاعات پایانی در گیت (git trailer format)](https://git-scm.com/docs/git-interpret-trailers) پیروی کنند.

انواع اضافی توسط استاندارد کامیت‌های قراردادی (Conventional Commits) اجباری نیستند و به‌صورت پیش‌فرض تأثیری در نسخه‌بندی معنایی (SemVer) ندارند (مگر اینکه شامل BREAKING CHANGE باشند).
<br /><br />
یک محدوده (scope) می‌تواند به یک نوع کامیت اختصاص یابد تا اطلاعات بیشتری در مورد زمینه تغییرات فراهم کند. این محدوده داخل پرانتز قرار می‌گیرد، مانند `feat(parser): add ability to parse arrays` که در آن "parser" بخشی از سیستم است که تغییرات در آن انجام شده.

## مثال‌ها

### پیام کامیت با توضیحات (description) و پاورقی تغییرات مهم (breaking change footer).
```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### پیام کامیت با علامت `!` برای جلب توجه به تغییرات مهم (breaking change).
```
feat!: send an email to the customer when a product is shipped
```

### پیام کامیت با محدوده و علامت `!` برای جلب توجه به تغییرات مهم (breaking change).
```
feat(api)!: send an email to the customer when a product is shipped
```

### پیام کامیت با علامت `!` و هم پاورقی (footer) BREAKING CHANGE برای جلب توجه به تغییرات مهم.
```
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

### پیام کامیت بدون بدنه
```
docs: correct spelling of CHANGELOG
```

### پیام کامیت با محدوده
```
feat(lang): add Polish language
```

### پیام کامیت با بدنه چند پاراگرافی و پاورقی (footer) های متعدد
```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Reviewed-by: Z
Refs: #123
```

## توضیحات کامل

1. کامیت‌ها _باید_ با یک نوع (type) شروع شوند که شامل یک اسم مانند `feat`، `fix` و... است. پس از آن، یک محدوده _اختیاری_ (scope) در پرانتز، یک علامت _اختیاری_ `!` (برای تغییرات مهم)، و در نهایت یک دو‌نقطه و فاصله _اجباری_ (`:`) می‌آید.
2. نوع `feat` باید زمانی استفاده شود که یک کامیت، یک ویژگی جدید به برنامه یا کتابخانه شما اضافه می‌کند.
3. نوع `fix` باید زمانی استفاده شود که یک کامیت نشان‌دهنده‌ی اصلاح یک باگ در برنامه شما باشد.
4. یک محدوده (scope) می‌تواند پس از نوع کامیت نوشته شود. محدوده باید شامل یک اسم باشد که بخشی از کدبیس را توصیف می‌کند و درون پرانتز قرار می‌گیرد، مانند: <span dir="ltr">`fix(parser):`</span>
5. توضیحات باید بلافاصله پس از دو نقطه و فاصله‌ی بعد از پیشوند نوع (type) یا محدوده (scope) بیاید.
توضیحات یک خلاصه کوتاه از تغییرات کد است، مثلاً:
_`fix: array parsing issue when multiple spaces were contained in string`_.
1. یک بدنه کامیت طولانی‌تر می‌تواند پس از توضیحات کوتاه نوشته شود تا اطلاعات زمینه‌ای بیشتری درباره تغییرات کد فراهم کند. بدنه باید بعد از یک خط خالی پس از توضیحات شروع شود.
2. بدنه کامیت دارای ساختار آزاد است و می‌تواند شامل هر تعداد پاراگراف جداشده با خط جدید باشد.
3. یک یا چند پاورقی (footer) می‌توانند در یک خط خالی پس از بدنه نوشته شوند. هر پاورقی باید شامل یک کلمه کلیدی، سپس <span dir="ltr">`:<space>` یا `<space>#`</span> ، و در نهایت یک مقدار رشته‌ای باشد (الهام گرفته از [git trailer convention](https://git-scm.com/docs/git-interpret-trailers)).
4. توکن (کلمه کلیدی) در پاورقی (footer) باید به جای فاصله از `-` استفاده کند، مانند `Acked-by` (این کار به تمایز بخش فوتر از یک بدنه چندپاراگرافی کمک می‌کند). یک استثنا برای `BREAKING CHANGE` وجود دارد که می‌تواند به عنوان یک توکن (کلمه کلیدی) استفاده شود.
5.  مقدار یک پاورقی (footer) می‌تواند شامل فاصله‌ها و خطوط جدید باشد، اما هنگام پردازش آن، اگر سیستم به یک پاورقی معتبر جدید برسد، پردازش متوقف می‌شود.
6.  تغییرات مهم (breaking changes) باید در پیشوند نوع (type) یا محدوده (scope) کامیت یا به عنوان یک توکن (کلمه کلیدی) در پاورقی (footer) مشخص شوند.
7.  اگر تغییرات مهم (Breaking Change) به عنوان یک پاورقی (footer) درج شود، باید شامل متن `BREAKING CHANGE` با حروف بزرگ، به همراه دو نقطه، یک فاصله و توضیحات باشد، مانند:
_`BREAKING CHANGE: environment variables now take precedence over config files.`_
1.  اگر تغییرات مهم (Breaking Change) در پیشوند نوع (type) یا محدوده (scope) قرار گیرد، باید با `!` بلافاصله قبل از `:` مشخص شود. در این صورت، درج `BREAKING CHANGE:` در پاورقی (footer) اختیاری است و توضیحات کامیت برای توصیف تغییرات مهم باید استفاده شود.
2.  انواع دیگری غیر از `feat` و `fix` می‌توانند استفاده شوند، مانند: _`docs: update ref docs.`_
3.  اجزای کامیت های قراردادی (Conventional Commits) به جز `BREAKING CHANGE` نباید به بزرگی و کوچکی حروف حساس باشند.
4.  BREAKING-CHANGE باید معادل BREAKING CHANGE در پاورقی (footer) در نظر گرفته شود.

## چرا از کامیت های قراردای استفاده کنیم؟

* تولید خودکار CHANGELOG
* تعیین خودکار افزایش نسخه‌بندی معنایی (semantic version) بر اساس انواع کامیت‌ها
* ارتباط بهتر تغییرات با هم‌تیمی‌ها، عموم و ذینفعان دیگر
* فعال‌سازی فرآیندهای ساخت و انتشار (build & publish)
* ایجاد یک تاریخچه‌ی کامیت ساختاریافته برای کمک به مشارکت‌کنندگان پروژه

## سوالات متداول

### چگونه باید در مرحله‌ی اولیه‌ی توسعه با پیام‌های کامیت برخورد کنم؟

توصیه می‌شود که پیام‌های کامیت را طوری بنویسید که انگار محصول شما از قبل منتشر شده است. معمولاً _کسی_ ، حتی اگر فقط همکاران توسعه‌دهنده‌ی شما باشند، از نرم‌افزار شما استفاده می‌کند. آن‌ها می‌خواهند بدانند چه مشکلاتی برطرف شده، چه تغییراتی اعمال شده و چه چیزی ممکن است باعث مشکلات جدید شود.

### آیا نوع (type) در عنوان کامیت باید با حروف بزرگ باشد یا کوچک؟

هر نوع حروفی (بزرگ یا کوچک) می‌تواند استفاده شود، اما بهتر است در پروژه خود از یک سبک ثابت پیروی کنید.

### اگر کامیت به بیش از یک نوع از انواع کامیت‌ها مطابقت داشته باشد، چه کار کنم؟

هر زمان که ممکن است، به عقب برگردید و کامیت‌ها را به صورت جداگانه بسازید. یکی از مزایای کامیت های قراردادی (Conventional Commits) این است که ما را به انجام کامیت‌ها و درخواست‌های `pull` سازمان‌یافته‌تر سوق می‌دهد.

### آیا این مانع از توسعه و تکرار سریع نمی‌شود؟

این فقط از حرکت سریع به روشی بی‌نظم جلوگیری می‌کند. این روش به شما کمک می‌کند تا در طولانی‌مدت و در پروژه‌های مختلف با مشارکت‌کنندگان متنوع، سریع حرکت کنید و در عین حال نظم و ترتیب را حفظ کنید.

### آیا ممکن است که کامیت‌های قراردادی (Conventional Commits) باعث شود که توسعه‌دهندگان محدود به نوع خاصی از کامیت‌ها شوند، چون به انواع مشخصی فکر می‌کنند؟

کامیت‌های قراردادی ما را تشویق می‌کند که بیشتر، کامیت‌هایی مانند اصلاحات انجام دهیم. به‌طور کلی، انعطاف‌پذیری کامیت‌های قراردادی این امکان را می‌دهد که تیم شما انواع (types) خاص خود را ایجاد کرده و این انواع را به مرور زمان تغییر دهد.

### چطور این به SemVer (نسخه‌بندی معنایی) مرتبط می‌شود؟

کامیت‌های نوع `fix` باید به به‌روزرسانی‌های `PATCH` تبدیل شوند. کامیت‌های نوع `feat` باید به به‌روزرسانی‌های `MINOR` تبدیل شوند. کامیت‌هایی که شامل `BREAKING CHANGE` هستند، بدون توجه به نوع کامیت، باید به به‌روزرسانی‌های `MAJOR` تبدیل شوند.

### چه کار کنم اگر اشتباهاً از نوع کامیت اشتباهی استفاده کردم؟

#### وقتی که از نوع صحیح استفاده نکردید، مثلاً `fix` به جای `feat`

قبل از ادغام (merge) یا انتشار (release) اشتباه، توصیه می‌کنیم از دستور `git rebase -i` برای ویرایش تاریخچه کامیت‌ها استفاده کنید. پس از انتشار، روش‌های تمیزکاری بسته به ابزارها و فرآیندهای شما متفاوت خواهد بود.

#### زمانی که از نوعی استفاده کردید که مطابق با استانداردها نیست، مثلاً `feet` به جای `feat`

در بدترین حالت، اگر یک کامیت که مطابق با استاندارد کامیت های قراردادی (Conventional Commits) نباشد، این پایان دنیا نیست. به سادگی آن کامیت توسط ابزارهایی که بر اساس استانداردها کار می‌کنند، نادیده گرفته می‌شود.

### آیا همه مشارکت‌کنندگان من باید از استاندارد های کامیت های قراردادی (Conventional Commits) استفاده کنند؟

نه! اگر از یک فرآیند مبتنی بر squash در Git استفاده کنید، نگه‌دارندگان اصلی (lead maintainers) می‌توانند هنگام ادغام (merge) پیام‌های کامیت را اصلاح کنند، بدون اینکه کار اضافی به مشارکت‌کنندگان عادی تحمیل شود.

یک روش رایج این است که سیستم Git شما به‌طور خودکار کامیت یک pull request را squash کند و سپس یک فرم برای نگه‌دارنده اصلی نمایش دهد تا پیام کامیت مناسب را برای ادغام وارد کند.

### کامیت های قراردادی (Conventional Commits) چگونه با برگرداندن (revert) کامیت‌ها برخورد می‌کند؟

برگرداندن (revert) کد می‌تواند پیچیده باشد؛ آیا چندین کامیت را برمی‌گرداند؟ اگر یک feature را برگرداند، آیا انتشار بعدی باید patch باشد؟

کامیت های قراردادی (Conventional Commits) رفتار مشخصی برای revert تعریف نکرده است. در عوض، به نویسندگان ابزارها اجازه می‌دهد تا با استفاده از انعطاف‌پذیری انواع (types) و پاورقی‌ها (footers)، منطق خود را برای مدیریت reverts توسعه دهند.

یک پیشنهاد این است که از نوع `revert` استفاده کنید و در پاورقی (footer)، SHA کامیت‌هایی که برگردانده شده‌اند را مشخص کنید.

```
revert: let us never again speak of the noodle incident

Refs: 676104e, a215868
```
