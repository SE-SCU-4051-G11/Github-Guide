# Merge در Git

## Merge چیست؟

Merge یعنی ادغام تغییرات یک Branch در Branch دیگر. معمولاً بعد از تمام شدن کار روی یک Branch جداگانه، آن را به Branch اصلی (`main`) ادغام می‌کنیم.

## Fast-forward

وقتی Branch اصلی بعد از ساخت Branch جدید تغییری نکرده باشد، Git فقط اشاره‌گر `main` را جلو می‌برد و Commit جدیدی نمی‌سازد. تاریخچه خطی می‌ماند.

## Merge commit

وقتی هر دو Branch بعد از جدا شدن Commit جدید داشته باشند، Git یک Commit جدید با دو والد می‌سازد که تاریخچه هر دو را نگه می‌دارد.

## تفاوت این دو

- Fast-forward: Commit جدید نمی‌سازد و تاریخچه خطی است.
- Merge commit: یک Commit جدید می‌سازد و مسیر هر Branch در تاریخچه دیده می‌شود.


## دستور git merge

اول به Branch مقصد بروید، بعد Branch مبدأ را Merge کنید:

```bash
git checkout main
git pull origin main
git merge docs/merging
```

برای دیدن تاریخچه:

```bash
git log --oneline --graph --all
```

## Merge از طریق Pull Request

در GitHub سه گزینه Merge وجود دارد:

- **Create a merge commit:** تاریخچه کامل حفظ می‌شود (در این پروژه از این گزینه استفاده می‌کنیم).
- **Squash and merge:** همه Commitها یکی می‌شوند.
- **Rebase and merge:** Commitها روی main دوباره چیده می‌شوند.

## Conflict چیست؟

وقتی دو نفر یک خط از یک فایل را به دو شکل متفاوت تغییر می‌دهند، Git نمی‌داند کدام را نگه دارد و Conflict ایجاد می‌کند. حل آن دستی است.