FluentoApp – Core Framework Plan (Backend + Frontend)

Bu bölüm, FluentoApp’in tüm modüllerinin üzerinde çalışacağı temel yazılım çatısını tanımlar. Hem .NET Core 8 Web API (Backend) hem de Flutter (Frontend) tarafı için yapılandırılmıştır. Tüm modüller, bu mimariye bağlı kalmalıdır.

🧠 1. BACKEND FRAMEWORK (.NET 8 Web API)

🎯 Genel Prensipler

Clean Architecture

Layered separation (API / Application / Domain / Infrastructure)

RESTful + versioned endpoints

📦 Temel Modüller

1.1 Authentication

Kullanıcı kayıt, giriş, refresh token desteği

JWT Token üretimi ve doğrulaması

OAuth2 destekli sosyal giriş (Google / Apple)

1.2 Authorization

Role-based auth (admin, user, guest)

Feature-based permission: hasFeature("feature_ai_feedback")

Policy-based attribute yönetimi

1.3 Logging

Serilog + File + Console + Seq desteği

Kullanıcı bazlı işlem izleme

1.4 Error Handling

Global UseExceptionHandler

Özel ApiException, ValidationException, UnauthorizedException

Hatalarda stack trace gizlenmeli, loglanmalı

1.5 Caching

MemoryCache (default)

Redis opsiyonel altyapı

[OutputCache] veya IMemoryCache bazlı yapı

1.6 Input Validation

FluentValidation + DataAnnotations

API endpoint başında ModelState.IsValid kontrolü

1.7 Swagger + Versioning

Swagger UI v2 aktif olmalı

Bearer token test desteği

v1, v2 route versioning

1.8 Rate Limiting

Kullanıcı ID + IP bazlı sınırlama

AspNetCoreRateLimit ile uygulanır

1.9 Common Responses

APIResponse yapısı: success, error, data, message

1.10 HealthCheck

/healthz endpoint üzerinden servis durumu kontrolü

1.11 Multilingual API Support

Accept-Language header desteklenmeli

📱 2. FRONTEND FRAMEWORK (Flutter + Dart)

🎯 Genel Prensipler

Feature-based klasörleme (modules: speaking, writing, etc.)

Reusable widgets

Mobile-first, offline-ready

📦 Temel Yapılar

2.1 Authentication Layer

Token bazlı giriş

flutter_secure_storage ile güvenli saklama

Biometrik giriş opsiyonu (local_auth)

2.2 State Management

Riverpod (provider override, async support)

go_router ile modüler navigasyon

2.3 Network Layer

Dio + Interceptors (token ekleme, error handler)

Retry mekanizması + loglama

2.4 UI Framework

Base AppCard, AppTextInput, AppButton, AppModal

Theme tanımı (dark/light, renk, padding, border)

Responsive grid desteği

2.5 Error Dialog & Logging

Standart showErrorDialog(context, error) fonksiyonu

AppLogger → konsol, remote log

2.6 Permission Management

Notification, mic, biometric izinleri request + check

2.7 Local Storage

Hive: offline cache

SharedPreferences: ayar tutma

2.8 Localization

intl paketi + JSON tabanlı çeviri dosyaları

2.9 Analytics (opsiyonel)

Firebase Analytics / Mixpanel desteği

🔐 3. GÜVENLİK STANDARTLARI

Alan

Önlem / Teknoloji

API Erişimi

JWT Bearer Token + IP rate limit

UI Yetkisi

Feature gating (UI buton gizleme)

Token Saklama

flutter_secure_storage

Biometrik

local_auth (PIN / TouchID)

Input

XSS/Injection temizliği, validation

AI Kullanımı

Açık rıza zorunluluğu (GDPR/KVKK)

Veritabanı

SQL log sansürleme, sadece gerekli alanları döndürme
