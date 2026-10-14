# legaleader-cron

Đồng hồ (cron) miễn phí cho bot **LegaLeader** (thu thập & đăng tin pháp luật/luật VN).

Giống `tvpl-cron`: Vercel Hobby chỉ cho cron 1 lần/ngày và serverless không tự chạy
vòng lặp, nên repo này dùng **GitHub Actions** gọi endpoint Vercel đều đặn.

Repo chỉ chứa 2 workflow + file này; **không chứa mã bot hay bí mật nào**
(token nằm trong GitHub Secret `RUN_BASE` và `CRON_TOKEN`).

## Endpoint được gọi

`GET {RUN_BASE}?job=<job>&token=<CRON_TOKEN>` — với `RUN_BASE` = `https://legaleader-bot-<scope>.vercel.app/api/run`

| job            | Việc                                              |
|----------------|---------------------------------------------------|
| `realtime`      | vnexpress → AI → đăng website (mỗi 5 phút)         |
| `email-approve` | quét email duyệt → đăng LinkedIn (mỗi 5 phút)      |

Các job 1 lần/ngày (`legal-update`, `daily-post`) chạy bằng GitHub Actions trong
repo private `legaleader-bot`, không qua đây.
