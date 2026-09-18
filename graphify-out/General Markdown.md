---
tags:
  - spec
  - oop
  - goal-management
  - task-management
  - reminder
  - obsidian
aliases:
  - Goal Task Management System
  - Hệ thống Quản lý Mục tiêu & Nhiệm vụ
status: draft
created: 2026-09-18
---

# Đặc tả Hệ thống Quản lý Mục tiêu & Nhiệm vụ

> [!abstract] Tóm tắt
> Hệ thống cho phép người dùng tạo **mục tiêu** và **nhiệm vụ** — bao gồm nhiệm vụ lặp lại — đồng thời đặt các thuộc tính như **độ ưu tiên**, **năng suất/chi phí nỗ lực**, thời hạn và tần suất. Ứng dụng sẽ quản lý, lập lịch, nhắc nhở và theo dõi tiến độ nhằm đảm bảo mục tiêu được hoàn thành.

---

## 1. Mục tiêu hệ thống

- Cho phép người dùng tạo, sửa, xóa mục tiêu.
- Cho phép tạo nhiệm vụ một lần hoặc lặp lại theo quy tắc.
- Gán nhiệm vụ vào mục tiêu.
- Đặt thuộc tính cho mục tiêu và nhiệm vụ:
  - Độ ưu tiên.
  - Năng suất/chi phí nỗ lực.
  - Thời hạn.
  - Tần suất lặp.
  - Kênh nhắc nhở.
- Tự động sinh lịch thực hiện và nhắc nhở.
- Theo dõi tiến độ mục tiêu.
- Cảnh báo khi mục tiêu có nguy cơ trễ.
- Hỗ trợ nhắc nhở thích ứng dựa trên hành vi hoàn thành.

---

## 2. Actor

| Actor | Vai trò |
|---|---|
| Người dùng | Tạo mục tiêu, nhiệm vụ, nhận nhắc nhở, đánh dấu hoàn thành |
| Scheduler | Lập lịch sinh occurrence và nhắc nhở |
| NotificationService | Gửi thông báo qua push/email/in-app |
| ProgressTracker | Tính toán tiến độ mục tiêu |
| GoalManager | Điều phối nghiệp vụ liên quan đến mục tiêu |
| TaskManager | Điều phối nghiệp vụ liên quan đến nhiệm vụ |

---

## 3. Use Case chính

- [ ] Tạo mục tiêu với độ ưu tiên, deadline, ngân sách năng suất.
- [ ] Tạo nhiệm vụ một lần.
- [ ] Tạo nhiệm vụ lặp lại.
- [ ] Gán nhiệm vụ vào mục tiêu.
- [ ] Đặt năng suất/chi phí nỗ lực cho nhiệm vụ.
- [ ] Sinh các lần thực hiện nhiệm vụ.
- [ ] Gửi nhắc nhở trước hạn.
- [ ] Gửi nhắc nhở lặp lại khi chưa hoàn thành.
- [ ] Đánh dấu hoàn thành nhiệm vụ.
- [ ] Cập nhật tiến độ mục tiêu.
- [ ] Cảnh báo mục tiêu quá tải hoặc trễ hạn.
- [ ] Điều chỉnh lịch và nhắc nhở thích ứng.

---

## 4. Mô hình miền hướng đối tượng

### 4.1. Sơ đồ lớp

```mermaid
classDiagram
    direction LR

    class User {
        +UUID id
        +String name
        +String email
        +String timezone
        +ProductivityProfile productivityProfile
        +createGoal(title, priority, deadline) Goal
        +createTask(goalId, taskSpec) Task
    }

    class Goal {
        +UUID id
        +String title
        +String description
        +Priority priority
        +GoalStatus status
        +DateTime deadline
        +Progress progress
        +ProductivityBudget budget
        +List~Task~ tasks
        +addTask(Task task)
        +removeTask(UUID taskId)
        +calculateProgress() Progress
        +isCompleted() bool
    }

    class Task {
        <<abstract>>
        +UUID id
        +String title
        +String description
        +Priority priority
        +TaskStatus status
        +Effort estimatedEffort
        +UUID goalId
        +complete()
        +reschedule(DateTime newDate)
    }

    class OneTimeTask {
        +DateTime dueDate
    }

    class RecurringTask {
        +RecurrenceRule recurrenceRule
        +generateOccurrences() List~TaskOccurrence~
    }

    class TaskOccurrence {
        +UUID id
        +UUID taskId
        +DateTime dueDate
        +TaskStatus status
        +DateTime completedAt
        +complete()
        +skip()
    }

    class RecurrenceRule {
        +Frequency frequency
        +int interval
        +List~String~ daysOfWeek
        +DateTime endDate
        +int count
        +nextOccurrence(DateTime after) DateTime
    }

    class Priority {
        +int level
        +String label
        +compareTo(Priority other) int
    }

    class Effort {
        +double amount
        +String unit
        +add(Effort other) Effort
    }

    class ProductivityProfile {
        +double dailyCapacity
        +String workingHours
        +String energyPattern
        +canFit(Effort effort) bool
        +allocate(TaskOccurrence occurrence) void
    }

    class ProductivityBudget {
        +double total
        +double used
        +remaining() double
        +consume(Effort effort) void
        +isExceeded() bool
    }

    class Reminder {
        +UUID id
        +DateTime remindAt
        +String message
        +ReminderChannel channel
        +ReminderStatus status
        +trigger()
        +snooze(Duration duration)
    }

    class ReminderPolicy {
        <<interface>>
        +generateReminders(TaskOccurrence occurrence) List~Reminder~
    }

    class Scheduler {
        +schedule(TaskOccurrence occurrence)
        +tick(DateTime now)
    }

    class NotificationService {
        <<interface>>
        +send(Reminder reminder)
    }

    class ProgressTracker {
        +updateProgress(UUID goalId)
        +calculate(Goal goal) Progress
    }

    class GoalManager {
        +createGoal(GoalSpec spec) Goal
        +assignTask(UUID goalId, Task task)
        +evaluateGoal(UUID goalId) GoalEvaluation
    }

    class TaskManager {
        +createTask(TaskSpec spec) Task
        +completeOccurrence(UUID occurrenceId)
        +rescheduleTask(UUID taskId, DateTime newDate)
    }

    User "1" --> "1" ProductivityProfile : has
    User "1" --> "*" Goal : owns
    Goal "1" o-- "*" Task : contains
    Task <|-- OneTimeTask
    Task <|-- RecurringTask
    RecurringTask "1" --> "1" RecurrenceRule : uses
    Task "1" --> "*" TaskOccurrence : generates
    TaskOccurrence "1" --> "*" Reminder : has
    Goal "1" --> "1" ProductivityBudget : has
    Task "1" --> "1" Effort : has
    ReminderPolicy ..> Reminder : creates
    Scheduler ..> ReminderPolicy : uses
    Scheduler ..> NotificationService : uses
    GoalManager ..> Goal : manages
    TaskManager ..> Task : manages
    ProgressTracker ..> Goal : tracks