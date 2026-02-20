# Value-Deadline-Priority-Scheduler-Simulation
# Value Density Scheduler Simulation  
شبیه‌سازی زمان‌بندی فرآیندها با معیار ارزش-چگالی (Value / Deadline)

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)
![Concurrency](https://img.shields.io/badge/Concurrency-Multi--threading-orange)
![Real--time](https://img.shields.io/badge/Paradigm-Real--time%20Scheduling-purple)
![License](https://img.shields.io/badge/License-MIT-green)

## درباره پروژه

این پروژه یک شبیه‌سازی **زمان‌بندی real-time** است که در آن فرآیندها بر اساس معیار **value density** (نسبت امتیاز ارزش به زمان باقی‌مانده تا deadline) اولویت‌بندی می‌شوند.

ویژگی‌های اصلی:

- تولید تصادفی فرآیندها با ارزش (value_score)، زمان اجرا و پنجره deadline
- استفاده از **value density** = `value_score / ending_deadline` به عنوان معیار اصلی اولویت
- **Admission control** با صف آماده محدود (MAX_READY_QUEUE_SIZE)
- **جایگزینی فرآیند ضعیف‌تر** (eviction) وقتی صف آماده پر است
- **چند هسته‌ای (multi-CPU)** – اجرای غیر پیش‌دستانه (non-preemptive) روی چند thread جداگانه
- رد شدن فرآیندهایی که deadline از دست رفته یا از صف آماده بیرون رانده شده‌اند
- محاسبه مجموع امتیاز موفق / ناموفق و میانگین زمان انتظار

مناسب برای دانشجویان مهندسی کامپیوتر، درس‌های **سیستم‌عامل**، **زمان‌بندی real-time**، **کنترل پذیرش (admission control)** و یادگیری concurrency در پایتون.

## الگوریتم اصلی تصمیم‌گیری

1. فرآیند جدید → محاسبه value density
2. اگر صف آماده (priority queue) جا داشته باشد → پذیرش
3. اگر پر باشد → مقایسه با **بدترین** فرآیند فعلی در صف
   - اگر فرآیند جدید بهتر است → جایگزینی (eviction) و فرآیند قدیمی fail می‌شود
4. CPUها همیشه بهترین فرآیند ممکن (با بررسی feasibility deadline) را انتخاب می‌کنند
5. فرآیندهایی که deadline از دست می‌دهند → فوراً fail می‌شوند

## نحوه اجرا

```bash
# کلون کردن پروژه
git clone https://github.com/your-username/value-density-scheduler-simulation.git
cd value-density-scheduler-simulation

# اجرا (به مدت حدود ۱ دقیقه شبیه‌سازی می‌کند)
python main.py
# یا اگر اسم فایل را تغییر دادید:
python scheduler_simulation.py
