# Graph Report - graphify  (2026-09-18)

## Corpus Check
- Corpus is ~26,189 words - fits in a single context window. You may not need a graph.

## Summary
- 91 nodes · 259 edges · 7 communities
- Extraction: 98% EXTRACTED · 2% INFERRED · 0% AMBIGUOUS · INFERRED: 4 edges (avg confidence: 0.82)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Reminder & Thông báo
- Onboarding & Điều hướng chính
- Theo dõi & Điều phối nền
- Thói quen & Chu kỳ lặp
- Tạo mục tiêu & Kiến trúc
- Nhiệm vụ, Ưu tiên & Lộ trình
- Prompt & Knowledge Graph

## God Nodes (most connected - your core abstractions)
1. `Workflow 4 — Vòng lặp nhắc nhở & hoàn thành` - 24 edges
2. `MVP (Tuần 2-6)` - 18 edges
3. `TaskService` - 17 edges
4. `Goal (entity)` - 16 edges
5. `TaskInstance (entity)` - 16 edges
6. `Workflow 2 — Tạo mục tiêu` - 16 edges
7. `Workflow 3 — Sinh nhiệm vụ lặp lại` - 13 edges
8. `NotificationService` - 13 edges
9. `Habit (entity)` - 12 edges
10. `DashboardPage (Hôm nay)` - 12 edges

## Surprising Connections (you probably didn't know these)
- `ReminderPopup (overlay)` --semantically_similar_to--> `Cơ chế retry & fallback thông báo (3 lần, backoff 1m-5m-15m, fallback IN_APP)`  [INFERRED] [semantically similar]
  04-luot-man-hinh.md → 05-kien-truc-va-van-hanh.md
- `Chia việc subagent song song (1 subagent / 1 file)` --semantically_similar_to--> `Chia việc theo subagent/parallel trong triển khai`  [INFERRED] [semantically similar]
  00-PROMPT-PLAN-KY-THUAT.md → 06-lo-trinh-trien-khai.md
- `Triết lý thiết kế mô hình miền (Entity / Service / Value Object)` --semantically_similar_to--> `Kiến trúc phân lớp Client - API - Application - Domain - Infrastructure`  [INFERRED] [semantically similar]
  02-mo-hinh-huong-doi-tuong.md → 05-kien-truc-va-van-hanh.md
- `ReminderScheduler (Scheduler / Reminder Engine worker)` --references--> `UC-06 Sinh TaskInstance định kỳ`  [EXTRACTED]
  05-kien-truc-va-van-hanh.md → 01-tong-quan-he-thong.md
- `Workflow 4 — Vòng lặp nhắc nhở & hoàn thành` --implements--> `UC-11 Kéo-thả đổi lịch`  [EXTRACTED]
  03-workflow-he-thong.md → 01-tong-quan-he-thong.md

## Hyperedges (group relationships)
- **Vòng lặp nhắc nhở & hoàn thành (Workflow 4)** — graphify_03_workflow_he_thong_workflow_4_vong_lap_nhac_nho_hoan_thanh, graphify_05_kien_truc_va_van_hanh_reminderscheduler, graphify_05_kien_truc_va_van_hanh_reminderservice, graphify_05_kien_truc_va_van_hanh_notificationservice, graphify_04_luot_man_hinh_reminderpopup, graphify_02_mo_hinh_huong_doi_tuong_taskinstance, graphify_02_mo_hinh_huong_doi_tuong_progresslog, graphify_02_mo_hinh_huong_doi_tuong_streak [EXTRACTED 1.00]
- **Phễu LandingPage → AuthPage → OnboardingPage → MainPage (Workflow 1)** — graphify_04_luot_man_hinh_landingpage, graphify_04_luot_man_hinh_authpage, graphify_04_luot_man_hinh_onboardingpage, graphify_04_luot_man_hinh_mainpage, graphify_03_workflow_he_thong_workflow_1_onboarding_dang_ky, graphify_02_mo_hinh_huong_doi_tuong_user [EXTRACTED 1.00]
- **Kiến trúc phân lớp Client - API - Application - Domain - Infrastructure của GHM** — graphify_05_kien_truc_va_van_hanh_client_spa_pwa, graphify_05_kien_truc_va_van_hanh_api_gateway, graphify_05_kien_truc_va_van_hanh_goalservice, graphify_05_kien_truc_va_van_hanh_taskservice, graphify_05_kien_truc_va_van_hanh_habitservice, graphify_05_kien_truc_va_van_hanh_reminderservice, graphify_05_kien_truc_va_van_hanh_analyticsservice, graphify_05_kien_truc_va_van_hanh_notificationservice, graphify_05_kien_truc_va_van_hanh_postgresql, graphify_05_kien_truc_va_van_hanh_redis_job_queue, graphify_05_kien_truc_va_van_hanh_reminderscheduler [EXTRACTED 1.00]

## Communities (7 total, 0 thin omitted)

### Community 0 - "Reminder & Thông báo"
Cohesion: 0.15
Nodes (19): Admin (tác nhân phụ), UC-07 Gửi Reminder đến hạn, UC-08 Hoàn thành / Skip nhiệm vụ, UC-09 Snooze / Dismiss Reminder, UC-10 Check-in Habit & cập nhật Streak, UC-12 Xem Dashboard & thống kê, UC-13 Nhận WeeklySummary, UC-14 Quản trị hệ thống (+11 more)

### Community 1 - "Onboarding & Điều hướng chính"
Cohesion: 0.22
Nodes (16): UC-01 Đăng ký tài khoản, UC-02 Đăng nhập, UC-03 Onboarding & thiết lập ban đầu, Goal (entity), GoalStatus (enum), User (entity), Workflow 1 — Onboarding & Đăng ký, AuthPage (Login / Register / ForgotPassword) (+8 more)

### Community 2 - "Theo dõi & Điều phối nền"
Cohesion: 0.33
Nodes (14): ProgressLog (entity), TaskInstance (entity), Workflow 5 — Tổng kết tuần, CalendarPage, GoalDetailPage, StatsPage, TaskFormModal (overlay), AnalyticsService (+6 more)

### Community 3 - "Thói quen & Chu kỳ lặp"
Cohesion: 0.35
Nodes (13): UC-06 Sinh TaskInstance định kỳ, Frequency (enum), Habit (entity), HabitType (enum), RecurrenceRule (value object), RecurringTask (entity), Streak (entity), Workflow 3 — Sinh nhiệm vụ lặp lại (+5 more)

### Community 4 - "Tạo mục tiêu & Kiến trúc"
Cohesion: 0.24
Nodes (12): UC-04 Tạo & quản lý Goal, UC-05 Tạo Task / RecurringTask, UC-11 Kéo-thả đổi lịch, Triết lý thiết kế mô hình miền (Entity / Service / Value Object), ProductivityMetric (value object), Workflow 2 — Tạo mục tiêu, GoalFormPage (create/edit), API Gateway (REST + JWT) (+4 more)

### Community 5 - "Nhiệm vụ, Ưu tiên & Lộ trình"
Cohesion: 0.28
Nodes (9): OneTimeTask (entity), Priority (enum), Task (abstract class), TaskStatus (enum), MoSCoW — khung phân loại ưu tiên, MVP (Tuần 2-6), Lộ trình triển khai GHM 12 tuần, Sprint 0 — Chuẩn bị (Tuần 1) (+1 more)

### Community 6 - "Prompt & Knowledge Graph"
Cohesion: 0.29
Nodes (8): Definition of Done, Knowledge Graph tài liệu GHM, Plan kỹ thuật (object model + workflow + UI flow + kiến trúc), Prompt gốc (người dùng), Prompt nâng cấp (System Designer / Software Architect), Chia việc subagent song song (1 subagent / 1 file), Goal Habit Manager (GHM), Chia việc theo subagent/parallel trong triển khai

## Ambiguous Edges - Review These
- `Workflow 2 — Tạo mục tiêu` → `Workflow 3 — Sinh nhiệm vụ lặp lại`  [AMBIGUOUS]
  03-workflow-he-thong.md · relation: conceptually_related_to

## Knowledge Gaps
- **13 isolated node(s):** `UC-01 Đăng ký tài khoản`, `UC-02 Đăng nhập`, `UC-03 Onboarding & thiết lập ban đầu`, `UC-04 Tạo & quản lý Goal`, `UC-05 Tạo Task / RecurringTask` (+8 more)
  These have ≤1 connection - possible missing edges or undocumented components.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **What is the exact relationship between `Workflow 2 — Tạo mục tiêu` and `Workflow 3 — Sinh nhiệm vụ lặp lại`?**
  _Edge tagged AMBIGUOUS (relation: conceptually_related_to) - confidence is low._
- **Why does `Workflow 4 — Vòng lặp nhắc nhở & hoàn thành` connect `Reminder & Thông báo` to `Onboarding & Điều hướng chính`, `Theo dõi & Điều phối nền`, `Thói quen & Chu kỳ lặp`, `Tạo mục tiêu & Kiến trúc`, `Prompt & Knowledge Graph`?**
  _High betweenness centrality (0.216) - this node is a cross-community bridge._
- **Why does `MVP (Tuần 2-6)` connect `Nhiệm vụ, Ưu tiên & Lộ trình` to `Reminder & Thông báo`, `Onboarding & Điều hướng chính`, `Theo dõi & Điều phối nền`, `Thói quen & Chu kỳ lặp`, `Tạo mục tiêu & Kiến trúc`?**
  _High betweenness centrality (0.143) - this node is a cross-community bridge._
- **Why does `Goal Habit Manager (GHM)` connect `Prompt & Knowledge Graph` to `Reminder & Thông báo`, `Onboarding & Điều hướng chính`, `Theo dõi & Điều phối nền`, `Thói quen & Chu kỳ lặp`, `Tạo mục tiêu & Kiến trúc`, `Nhiệm vụ, Ưu tiên & Lộ trình`?**
  _High betweenness centrality (0.129) - this node is a cross-community bridge._
- **What connects `UC-01 Đăng ký tài khoản`, `UC-02 Đăng nhập`, `UC-03 Onboarding & thiết lập ban đầu` to the rest of the system?**
  _13 weakly-connected nodes found - possible documentation gaps or missing edges._