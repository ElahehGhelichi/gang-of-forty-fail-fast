# راهنمای بازگشت نسخه‌ی production

## اجرای rollback از GitHub Actions

1. در مخزن فروشگاه، تب **Actions** را باز کنید.
2. از فهرست workflowها، **Roll back production** را انتخاب کنید.
3. **Run workflow** را بزنید و شاخه‌ی `main` را انتخاب کنید.
4. فیلد **Deployment URL** را خالی بگذارید تا Vercel به production قبلی برگردد. برای هدف‌گرفتن یک deployment مشخص، URL همان deployment تولیدی را وارد کنید.
5. اجرا را شروع کنید و پس از موفقیت، سایت production را باز کنید و مسیرهای اصلی و افزودن محصول به سبد را بررسی کنید.

این workflow به همان سه secret انتشار نیاز دارد: `VERCEL_TOKEN`، `VERCEL_ORG_ID` و `VERCEL_PROJECT_ID`. مقدار secretها در log چاپ نمی‌شود.

در پلن Hobby، Vercel فقط اجازه‌ی برگشت به deployment تولیدی قبلی را می‌دهد. برگشت به نسخه‌های قدیمی‌تر ممکن است به پلن Pro یا Enterprise نیاز داشته باشد. پس از rollback، برای برگشت به نسخه‌ی جدیدتر از گزینه‌ی **Undo Rollback** در داشبورد Vercel یا `vercel promote <deployment-url>` استفاده کنید؛ مستندات Vercel می‌گوید این کار اتصال خودکار دامنه به انتشارهای بعدی را دوباره فعال می‌کند.

## برچسب‌های Docker در GHCR

هر push موفق به `main`، ایمیج را با برچسب `latest` و `sha-<commit>` در GitHub Container Registry منتشر می‌کند. برای بازتولید دقیق یک نسخه، به‌جای `latest` برچسب commit را استفاده کنید:

```bash
docker pull ghcr.io/elahehghelichi/gang-of-forty-fail-fast:sha-abc1234
```

انتشار روی PR انجام نمی‌شود؛ job داکر در PR فقط image را build می‌کند تا تغییرها بدون نوشتن در registry بررسی شوند.
