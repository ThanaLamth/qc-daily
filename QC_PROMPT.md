# QC Prompt

Use this prompt in a fresh Codex profile when you want article QC output to match the detailed issue-by-issue CSV workflow used in `qc-daily`.

## Full Prompt

```text
Dùng skill `writing-qc` để review bài viết này và xuất kết quả theo đúng format CSV chi tiết như repo `qc-daily`.

Article URL:
<PASTE_URL_HERE>

Yêu cầu:
1. review thật chi tiết theo kiểu editorial QC
2. verdict phải là một trong:
   - Pass
   - Revise
   - Fail
3. mỗi issue phải có:
   - severity
   - category
   - issue_detail
   - why_it_matters
   - suggested_solution
4. chỉ coi `need for visual media` là issue khi mức cần là `high`
   - nếu không cần thì ghi rõ: `No supporting visual media needed`
5. tập trung vào:
   - factual accuracy
   - source quality
   - originality / added value
   - title-to-body match
   - heading / structure
   - internal-link relevance
   - trust signals
   - evidence clarity
   - readability
   - whether supporting visual media is clearly needed
6. output cuối phải gồm:
   - verdict tổng
   - detailed issues
   - highest-impact fixes
7. sau đó tạo file CSV theo format giống các file trong repo `qc-daily`

CSV columns:
- article_url
- site
- article_slug
- review_date
- verdict
- severity
- category
- issue_detail
- why_it_matters
- suggested_solution
- visual_media_need
- notes

Quy tắc:
- mỗi issue là 1 row
- verdict tổng lặp lại ở mỗi row
- nếu article không cần thêm media, ghi `No supporting visual media needed`
- không viết QC quá ngắn
- phải đủ chi tiết để editor sửa bài theo từng issue

Sau khi tạo CSV:
1. lưu vào repo local `qc-daily`
2. đặt tên file theo pattern:
   YYYY-MM-DD-site-slug-qc-issues.csv
3. commit
4. push lên GitHub repo `https://github.com/ThanaLamth/qc-daily`
5. trả lại URL GitHub của file
```

## Short Version

```text
$writing-qc <ARTICLE_URL>

Sau khi review, hãy:
- viết detailed QC như workflow hiện tại
- convert thành CSV issue list
- mỗi issue là 1 row
- fields bắt buộc:
  article_url, site, article_slug, review_date, verdict, severity, category, issue_detail, why_it_matters, suggested_solution, visual_media_need, notes
- chỉ flag visual media khi need = high
- nếu không cần, ghi `No supporting visual media needed`
- lưu vào repo local `/home/qcdaily/qc-daily`
- commit và push lên `https://github.com/ThanaLamth/qc-daily`
- trả về URL GitHub của file
```

## QC Logic

- `Fail`: có lỗi factual, legal, sourcing, hoặc trust issue nghiêm trọng ở core claim
- `Revise`: bài đúng intent nhưng còn yếu ở source, originality, analysis, trust, hoặc evidence clarity
- `Pass`: source tốt, có added value, structure ổn, trust signals đủ, không có lỗi lớn

## Default QC Style

- findings-first
- detailed issue-by-issue explanation
- concrete fix for every issue
- finance/policy topics require stricter sourcing
- use primary-source expectations where possible
