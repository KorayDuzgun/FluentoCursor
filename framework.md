 FluentoApp – Core Framework Plan (Backend + Frontend + DB + Security)
Bu yapı, FluentoApp’in tüm modüllerinin üzerine inşa edileceği temel yazılım çatısını tanımlar.
Kapsam:

Backend: ASP.NET Core 8 Web API

Frontend: Flutter

Veritabanı: PostgreSQL + Entity Framework Core

Güvenlik: Role-based + Feature-based + OWASP uyumlu

🧠 1. BACKEND FRAMEWORK (.NET 8 Web API)
🎯 Genel Prensipler
Clean Architecture

Layered separation (API / Application / Domain / Infrastructure)

RESTful + versioned endpoints

📦 Temel Modüller
✅ 1.1 Authentication
JWT + Refresh Token sistemi

OAuth2 (Google / Apple) desteği

Token içeriği: userId, email, role, featureKeys

✅ 1.2 Authorization
Role-based: guest, free_user, premium_user, admin

Feature-based access kontrol: örn. feature_ai_feedback, feature_tts_native

Authorize(Policy = "HasFeature:xyz") yapısı

✅ 1.3 Logging
Serilog: File + Seq + Console

Log context: userId, endpoint, responseTime

✅ 1.4 Exception Handling
Global middleware

Custom exceptions: ValidationException, ApiException

Log + mask sensitive details

✅ 1.5 Caching
MemoryCache (default)

Redis (opsiyonel)

Kullanıcıya özel cache key yapısı: cache:user:{id}:progress

✅ 1.6 Validation
FluentValidation

Centralized error response standard

✅ 1.7 Swagger + Versioning
v1, v2 endpoint ayrımı

Swagger UI + Bearer token testi

✅ 1.8 Rate Limiting
IP & userId bazlı sınır

AspNetCoreRateLimit middleware

✅ 1.9 Multilingual Support
Accept-Language header üzerinden içerik yönlendirme

📱 2. FRONTEND FRAMEWORK (Flutter)
📦 Temel Yapılar
✅ 2.1 Auth Layer
Login/Register akışı

flutter_secure_storage kullanarak token saklama

Biometric giriş (local_auth)

✅ 2.2 State Management
Riverpod

go_router ile modüler yönlendirme

✅ 2.3 Network Layer
Dio + Interceptors

Authorization header

Retry mekanizması

Global error handler

✅ 2.4 UI Framework
Reusable Widget’lar: AppCard, AppTextField, AppButton

Responsive layout

Theme + Typography + Padding standardizasyonu

✅ 2.5 Offline & Local Storage
Hive: user logs, cached kelime kartları

SharedPreferences: dil, ayar vs.

✅ 2.6 Permission Management
Mic, Notification, Biometric izni yöneticisi

🗃️ 3. VERİTABANI ŞEMASI (PostgreSQL – EF Core)
Tablo	Açıklama
Users	Id, Email, PasswordHash, Role, CreatedAt
Features	Id, Key, Description
UserFeatures	userId, featureId
Vocabulary	Word, Definition, POS, Synonyms, Antonyms, Example, Level
UserVocabulary	userId, vocabId, status (learned/review), exampleSentence, updatedAt
SpeakingPrompts	Sentence, Level
UserSpeakingLogs	userId, promptId, userText, aiCorrection, elapsedTime, createdAt
WritingPrompts	Topic, Level
UserWritingLogs	userId, promptId, text, aiCorrection, grammarTips, createdAt
ReadingPassages	Title, Content, Level, audioUrl
ReadingQuizzes	passageId, question, options[], correctIndex
UserReadingLogs	userId, passageId, answers[], score, duration
AssessmentSessions	userId, startedAt, status
AssessmentResults	userId, readingScore, writingLevel, vocabScore, overallLevel, createdAt
Achievements	Name, Criteria, Icon
UserProgressStats	userId, month, speakingTime, wordCount, correctRate

🔐 4. GÜVENLİK ÖNLEMLERİ
Alan	Önlem / Teknoloji
API erişimi	JWT Token + IP Rate Limit
UI yetkisi	Feature Gate: buton/ekran gizleme
Token güvenliği	flutter_secure_storage (AES)
Giriş işlemleri	Password hashing (bcrypt), OAuth2
AI servisleri	Prompt loglama + rate limit
Veri gizliliği	GDPR/KVKK uyumlu: data export/silme/consent
Admin işlemleri	2FA + IP safelisting önerilir
Database	Role separation (readonly/readwrite), minimal column exposure
XSS / SQL Injection	Input validation, parametreli sorgular
TTS ve Bildirim	Kullanıcıdan açık izin alınmalı (device & app)
