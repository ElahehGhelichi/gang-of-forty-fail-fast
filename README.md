# Fail-Fast Shop

[![CI](https://github.com/ElahehGhelichi/gang-of-forty-fail-fast/actions/workflows/deploy.yml/badge.svg)](https://github.com/ElahehGhelichi/gang-of-forty-fail-fast/actions/workflows/deploy.yml)

فروشگاه فارسی RTL ساخته‌شده با React، TypeScript و Vite.

## اجرای محلی

```bash
npm ci
npm run dev
```

## بررسی و ساخت

```bash
npm run ci
npm run build
```

## اجرای Docker

```bash
docker build -t fail-fast-shop .
docker run --rm -p 8080:80 --name fail-fast-shop fail-fast-shop
```

سپس `http://localhost:8080` را باز کنید. درخواست‌های `/api/` از طریق Nginx به API کاتالوگ هدایت می‌شوند.

## انتشار ایمیج در GHCR

با موفقیت workflow روی شاخه‌ی `main`، ایمیج در GitHub Container Registry منتشر می‌شود:

```bash
docker pull ghcr.io/elahehghelichi/gang-of-forty-fail-fast:latest
docker run --rm -p 8080:80 ghcr.io/elahehghelichi/gang-of-forty-fail-fast:latest
```

هر انتشار علاوه بر `latest`، با برچسب تغییرناپذیر `sha-<commit>` هم ذخیره می‌شود تا نسخه‌ی مشخصی قابل دریافت باشد.

## استقرار

این پروژه برای Vercel آماده شده است. در GitHub Actions، سه Secret زیر را برای مخزن اختصاصی فروشگاه تنظیم کنید:

- `VERCEL_TOKEN`
- `VERCEL_ORG_ID`
- `VERCEL_PROJECT_ID`

Pull Request به `main` یک پیش‌نمایش Vercel می‌سازد و push به `main` نسخه production را منتشر می‌کند. آدرس production را پس از deploy در `shop.json` ثبت کنید.

### بازگشت به نسخه‌ی قبلی

از تب **Actions**، workflow با نام **Roll back production** را باز کنید و **Run workflow** را بزنید. ورودی آدرس deployment اختیاری است: خالی بماند تا Vercel به production قبلی برگردد، یا URL یک deployment تولیدی را وارد کنید. بعد از پایان کار، آدرس production را بازبینی کنید. جزئیات و محدودیت پلن Hobby در [راهنمای rollback](docs/rollback.md) آمده است.

## بررسی موبایل و کیفیت

- [اسکرین‌شات موبایل (390×844)](docs/mobile.png)
- [خلاصه‌ی Lighthouse](docs/lighthouse.md)
- [گزارش کامل Lighthouse (HTML)](docs/lighthouse-report.report.html)
- [داده‌ی خام Lighthouse (JSON)](docs/lighthouse-report.report.json)

## مجوز و همکاری

این پروژه بخشی از بوت‌کمپ Gang of Forty است. راهنمای ساخت و نگهداری در `AGENTS.md` قرار دارد.
