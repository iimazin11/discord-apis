# 📚 Discord APIs Documentation - دليل شامل

## 📋 جدول المحتويات
1. [🔐 Authentication APIs](#-authentication-apis-apis-المصادقة)
2. [👤 User APIs](#-user-apis-apis-الخاصة-بالمستخدم)
3. [🤖 Bot APIs](#-bot-apis-apis-الخاصة-بالبوتات)
4. [🎮 Game & Hyper Squad APIs](#-game--hyper-squad-apis-ألعاب-وهايبر-سكواد)
5. [🏷️ Sticker APIs](#%EF%B8%8F-sticker-apis-الملصقات)
6. [👥 Thread APIs](#-thread-apis-المواضيعالخيوط)
7. [🎭 Stage Discovery APIs](#-stage-discovery-apis)
8. [📢 Announcement APIs](#-announcement-apis)
9. [🎵 Soundboard APIs](#-soundboard-apis-لوحة-الأصوات)
10. [💬 Forum APIs](#-forum-apis-المنتديات)
11. [🛡️ Safety & Analytics APIs](#%EF%B8%8F-safety--analytics-apis-الأمان-والتحليلات)
12. [🎫 Ticket APIs](#-ticket-apis-نظام-التذاكر)
13. [⚙️ Application APIs](#%EF%B8%8F-application-apis-التطبيقات)
14. [🔍 Search APIs](#-search-apis-البحث)
15. [📌 معلومات عامة](#-معلومات-عامة)

---

## 🔐 **Authentication APIs (APIs المصادقة)**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/oauth2/authorize` | GET | تفويض OAuth2 | `client_id`, `redirect_uri`, `scope`, `response_type` | صفحة تفويض | User |
| `/oauth2/token` | POST | الحصول على التوكن | `client_id`, `client_secret`, `grant_type`, `code`, `redirect_uri` | `{access_token, refresh_token, expires_in}` | User |
| `/oauth2/token/revoke` | POST | إلغاء التوكن | `client_id`, `client_secret`, `token` | `{}` | User |
| `/oauth2/@me` | GET | معلومات المستخدم الحالي | `Authorization: Bearer <token>` | معلومات المستخدم | User |

---

## 👤 **User APIs (APIs الخاصة بالمستخدم)**

### **معلومات المستخدم**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/users/@me` | GET | الحصول على بيانات الملف الشخصي | `Authorization: Bearer <token>` | معلومات المستخدم الكاملة | User |
| `/users/@me` | PATCH | تحديث بيانات المستخدم | `{username, avatar, bio, ...}` | معلومات المستخدم المحدثة | User |
| `/users/@me/connections` | GET | حسابات متصلة | `Authorization: Bearer <token>` | قائمة بالحسابات المتصلة | User |
| `/users/@me/guilds` | GET | السيرفرات المشترك فيها | `Authorization: Bearer <token>` | قائمة السيرفرات | User |
| `/users/@me/billing` | GET | معلومات الفواتير | `Authorization: Bearer <token>` | معلومات الاشتراكات | User |
| `/users/@me/affinities/users` | GET | المستخدمين المقربين | `Authorization: Bearer <token>` | قائمة المستخدمين المقربين | User |

### **الرسائل المباشرة**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/users/@me/channels` | GET | جلب قنوات الدردشة المباشرة | `Authorization: Bearer <token>` | قائمة القنوات | User |
| `/users/@me/channels` | POST | إنشاء دردشة مباشرة | `{recipient_id}` | معلومات القناة الجديدة | User |
| `/channels/{channel.id}/messages` | GET | جلب الرسائل | `Authorization: Bearer <token>` | قائمة الرسائل | User |
| `/channels/{channel.id}/messages` | POST | إرسال رسالة | `{content, embeds, components}` | الرسالة المرسلة | User |
| `/channels/{channel.id}/messages/{message.id}` | PUT | تعديل رسالة | `{content, embeds, components}` | الرسالة المعدلة | User |
| `/channels/{channel.id}/messages/{message.id}` | DELETE | حذف رسالة | `Authorization: Bearer <token>` | `{}` | User |

---

## 🤖 **Bot APIs (APIs الخاصة بالبوتات)**

### **الرئيسية للبوتات**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/gateway` | GET | بوابة WebSocket | `Authorization: Bot <token>` | `{url, shards}` | Bot |
| `/gateway/bot` | GET | معلومات البوابة للبوت | `Authorization: Bot <token>` | `{url, shards, session_start_limit}` | Bot |

### **السيرفرات (Guilds)**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/guilds/{guild.id}` | GET | معلومات السيرفر | `Authorization: Bot <token>` | معلومات السيرفر | Bot |
| `/guilds/{guild.id}` | PATCH | تعديل السيرفر | `{name, icon, region, ...}` | معلومات السيرفر المحدثة | Bot |
| `/guilds/{guild.id}` | DELETE | حذف السيرفر | `Authorization: Bot <token>` | `{}` | Bot |
| `/guilds/{guild.id}/channels` | GET | قنوات السيرفر | `Authorization: Bot <token>` | قائمة القنوات | Bot |
| `/guilds/{guild.id}/channels` | POST | إنشاء قناة | `{name, type, topic, ...}` | معلومات القناة الجديدة | Bot |
| `/guilds/{guild.id}/members` | GET | أعضاء السيرفر | `Authorization: Bot <token>` | قائمة الأعضاء | Bot |
| `/guilds/{guild.id}/members/{user.id}` | GET | معلومات عضو | `Authorization: Bot <token>` | معلومات العضو | Bot |
| `/guilds/{guild.id}/members/{user.id}` | PUT | تعديل العضو | `{nick, roles, mute, deaf}` | معلومات العضو المحدثة | Bot |
| `/guilds/{guild.id}/members/{user.id}` | DELETE | طرد عضو | `Authorization: Bot <token>` | `{}` | Bot |
| `/guilds/{guild.id}/bans` | GET | المحظورين | `Authorization: Bot <token>` | قائمة المحظورين | Bot |
| `/guilds/{guild.id}/bans/{user.id}` | PUT | حظر عضو | `{delete_message_days, reason}` | `{}` | Bot |
| `/guilds/{guild.id}/bans/{user.id}` | DELETE | إلغاء حظر | `Authorization: Bot <token>` | `{}` | Bot |
| `/guilds/{guild.id}/roles` | GET | رتب السيرفر | `Authorization: Bot <token>` | قائمة الرتب | Bot |
| `/guilds/{guild.id}/roles` | POST | إنشاء رتبة | `{name, permissions, color, ...}` | معلومات الرتبة الجديدة | Bot |
| `/guilds/{guild.id}/roles/{role.id}` | PATCH | تعديل رتبة | `{name, permissions, color, ...}` | معلومات الرتبة المحدثة | Bot |
| `/guilds/{guild.id}/roles/{role.id}` | DELETE | حذف رتبة | `Authorization: Bot <token>` | `{}` | Bot |

### **القنوات (Channels)**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/channels/{channel.id}` | GET | معلومات القناة | `Authorization: Bot <token>` | معلومات القناة | Both |
| `/channels/{channel.id}` | PATCH | تعديل القناة | `{name, topic, position, ...}` | معلومات القناة المحدثة | Bot |
| `/channels/{channel.id}` | DELETE | حذف القناة | `Authorization: Bot <token>` | `{}` | Bot |
| `/channels/{channel.id}/messages` | GET | جلب الرسائل | `Authorization: Bot <token>` | قائمة الرسائل | Both |
| `/channels/{channel.id}/messages` | POST | إرسال رسالة | `{content, embeds, components, tts}` | الرسالة المرسلة | Both |
| `/channels/{channel.id}/messages/{message.id}` | GET | جلب رسالة معينة | `Authorization: Bot <token>` | محتوى الرسالة | Both |
| `/channels/{channel.id}/messages/{message.id}` | PATCH | تعديل رسالة | `{content, embeds, components}` | الرسالة المعدلة | Both |
| `/channels/{channel.id}/messages/{message.id}` | DELETE | حذف رسالة | `Authorization: Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/messages/bulk-delete` | POST | حذف جماعي | `{messages: [id1, id2, ...]}` | `{}` | Bot |
| `/channels/{channel.id}/permissions/{overwrite.id}` | PUT | تعديل صلاحيات | `{allow, deny, type}` | `{}` | Bot |
| `/channels/{channel.id}/permissions/{overwrite.id}` | DELETE | حذف صلاحيات | `Authorization: Bot <token>` | `{}` | Bot |
| `/channels/{channel.id}/typing` | POST | مؤشر الكتابة | `Authorization: Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/pins` | GET | الرسائل المثبتة | `Authorization: Bot <token>` | قائمة الرسائل المثبتة | Both |
| `/channels/{channel.id}/pins/{message.id}` | PUT | تثبيت رسالة | `Authorization: Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/pins/{message.id}` | DELETE | إلغاء تثبيت رسالة | `Authorization: Bot <token>` | `{}` | Both |

### **التفاعلات (Interactions)**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/interactions/{interaction.id}/{interaction.token}/callback` | POST | الرد على Interaction | `{type, data}` | `{}` | Bot |
| `/webhooks/{application.id}/{interaction.token}/messages/@original` | GET | جلب الرد الأصلي | `Authorization: Bot <token>` | محتوى الرسالة | Bot |
| `/webhooks/{application.id}/{interaction.token}/messages/@original` | PATCH | تعديل الرد الأصلي | `{content, embeds, components}` | الرسالة المعدلة | Bot |
| `/webhooks/{application.id}/{interaction.token}/messages/@original` | DELETE | حذف الرد الأصلي | `Authorization: Bot <token>` | `{}` | Bot |
| `/webhooks/{application.id}/{interaction.token}` | POST | إنشاء متابعة للرد | `{content, embeds, components}` | الرسالة الجديدة | Bot |

### **Webhooks**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/webhooks/{webhook.id}` | GET | معلومات Webhook | `Authorization: Bot <token>` | معلومات Webhook | Bot |
| `/webhooks/{webhook.id}` | PATCH | تعديل Webhook | `{name, avatar, channel_id}` | معلومات Webhook المحدثة | Bot |
| `/webhooks/{webhook.id}` | DELETE | حذف Webhook | `Authorization: Bot <token>` | `{}` | Bot |
| `/webhooks/{webhook.id}/{webhook.token}` | POST | إرسال عبر Webhook | `{content, embeds, username, avatar_url}` | `{}` | Both |
| `/webhooks/{webhook.id}/{webhook.token}/messages/{message.id}` | PATCH | تعديل رسالة Webhook | `{content, embeds}` | الرسالة المعدلة | Bot |
| `/webhooks/{webhook.id}/{webhook.token}/messages/{message.id}` | DELETE | حذف رسالة Webhook | `Authorization: Bot <token>` | `{}` | Bot |

### **الأوامر التطبيقية (Application Commands)**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/applications/{application.id}/commands` | GET | جلب الأوامر العامة | `Authorization: Bot <token>` | قائمة الأوامر | Bot |
| `/applications/{application.id}/commands` | POST | إنشاء أمر عام | `{name, description, options}` | معلومات الأمر الجديد | Bot |
| `/applications/{application.id}/guilds/{guild.id}/commands` | GET | جلب أوامر السيرفر | `Authorization: Bot <token>` | قائمة الأوامر | Bot |
| `/applications/{application.id}/guilds/{guild.id}/commands` | POST | إنشاء أمر في السيرفر | `{name, description, options}` | معلومات الأمر الجديد | Bot |
| `/applications/{application.id}/guilds/{guild.id}/commands/{command.id}` | PATCH | تعديل أمر | `{name, description, options}` | معلومات الأمر المحدث | Bot |
| `/applications/{application.id}/guilds/{guild.id}/commands/{command.id}` | DELETE | حذف أمر | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🎮 **Game & Hyper Squad APIs (ألعاب وهايبر سكواد)**

### **هايبر سكواد (Hyper Squad)**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/activities` | GET | الأنشطة المتاحة | `Authorization: Bearer/Bot <token>` | قائمة الأنشطة | Both |
| `/activities/{activity.id}/sessions` | POST | بدء نشاط | `{max_age, max_uses, target_application_id}` | معلومات الجلسة | Both |
| `/channels/{channel.id}/invites` | POST | دعوة للنشاط | `{target_type, target_application_id}` | رابط الدعوة | Both |
| `/applications/{application.id}/entitlements` | GET | تراخيص التطبيق | `Authorization: Bot <token>` | قائمة التراخيص | Bot |
| `/store/skus` | GET | منتجات المتجر | `Authorization: Bearer <token>` | قائمة المنتجات | User |
| `/store/published-listings/skus/{sku.id}` | GET | تفاصيل المنتج | `Authorization: Bearer <token>` | تفاصيل المنتج | User |
| `/store/skus/{sku.id}/purchase` | POST | شراء منتج | `Authorization: Bearer <token>` | `{gift_code, gift_url}` | User |

### **ألعاب (Games)**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/users/@me/games` | GET | ألعاب المستخدم | `Authorization: Bearer <token>` | قائمة الألعاب | User |
| `/applications/{application.id}/store-listing` | GET | صفحة المتجر | `Authorization: Bearer <token>` | معلومات المتجر | User |
| `/applications/{application.id}/achievements` | GET | إنجازات اللعبة | `Authorization: Bot <token>` | قائمة الإنجازات | Bot |
| `/users/@me/applications/{application.id}/achievements` | GET | إنجازات المستخدم | `Authorization: Bearer <token>` | إنجازات المستخدم | User |
| `/applications/{application.id}/entitlements/gifts` | POST | إنشاء هدية | `Authorization: Bot <token>` | `{gift_code}` | Bot |

### **الأنشطة الصوتية (Voice Activities)**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/channels/{channel.id}/voice-status` | GET | حالة الصوت | `Authorization: Bearer <token>` | معلومات الصوت | User |
| `/channels/{channel.id}/voice-status/@me` | PUT | تحديث حالة الصوت | `{status}` | `{}` | User |
| `/applications/{application.id}/voice-states` | POST | تحديث حالة صوت التطبيق | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🏷️ **Sticker APIs (الملصقات)**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/stickers/{sticker.id}` | GET | معلومات الملصق | `Authorization: Bot <token>` | معلومات الملصق | Both |
| `/guilds/{guild.id}/stickers` | GET | ملصقات السيرفر | `Authorization: Bot <token>` | قائمة الملصقات | Both |
| `/guilds/{guild.id}/stickers/{sticker.id}` | GET | ملصق محدد | `Authorization: Bot <token>` | معلومات الملصق | Both |
| `/guilds/{guild.id}/stickers` | POST | إنشاء ملصق | `files[], {name, description, tags}` | معلومات الملصق الجديد | Bot |
| `/guilds/{guild.id}/stickers/{sticker.id}` | PATCH | تحديث ملصق | `{name, description, tags}` | معلومات الملصق المحدث | Bot |
| `/guilds/{guild.id}/stickers/{sticker.id}` | DELETE | حذف ملصق | `Authorization: Bot <token>` | `{}` | Bot |
| `/sticker-packs` | GET | حزم الملصقات | `Authorization: Bearer <token>` | قائمة الحزم | User |

---

## 👥 **Thread APIs (المواضيع/الخيوط)**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/channels/{channel.id}/threads` | POST | إنشاء موضوع | `{name, auto_archive_duration, type}` | معلومات الموضوع | Both |
| `/channels/{channel.id}/threads` | GET | المواضيع النشطة | `Authorization: Bot <token>` | قائمة المواضيع | Both |
| `/channels/{channel.id}/threads/archived/public` | GET | المواضيع المؤرشفة العامة | `Authorization: Bot <token>` | قائمة المواضيع | Both |
| `/channels/{channel.id}/threads/archived/private` | GET | المواضيع المؤرشفة الخاصة | `Authorization: Bot <token>` | قائمة المواضيع | Both |
| `/channels/{channel.id}/users/@me/threads/archived/private` | GET | مواضيعك المؤرشفة | `Authorization: Bearer <token>` | قائمة المواضيع | User |
| `/channels/{thread.id}/messages` | GET | رسائل الموضوع | `Authorization: Bot <token>` | قائمة الرسائل | Both |
| `/channels/{thread.id}/members` | GET | أعضاء الموضوع | `Authorization: Bot <token>` | قائمة الأعضاء | Both |
| `/channels/{thread.id}/members/@me` | PUT | الانضمام للموضوع | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{thread.id}/members/{user.id}` | PUT | إضافة عضو للموضوع | `Authorization: Bot <token>` | `{}` | Bot |
| `/channels/{thread.id}/members/@me` | DELETE | مغادرة الموضوع | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{thread.id}/members/{user.id}` | DELETE | إزالة عضو من الموضوع | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🎭 **Stage Discovery APIs**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/stage-instances` | POST | إنشاء Stage | `{channel_id, topic, privacy_level}` | معلومات Stage | Bot |
| `/stage-instances/{channel.id}` | GET | معلومات Stage | `Authorization: Bot <token>` | معلومات Stage | Bot |
| `/stage-instances/{channel.id}` | PATCH | تحديث Stage | `{topic, privacy_level}` | معلومات Stage المحدثة | Bot |
| `/stage-instances/{channel.id}` | DELETE | حذف Stage | `Authorization: Bot <token>` | `{}` | Bot |

---

## 📢 **Announcement Channels APIs**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/channels/{channel.id}/messages/{message.id}/crosspost` | POST | نشر إعلان | `Authorization: Bot <token>` | الرسالة المنشورة | Bot |
| `/channels/{channel.id}/followers` | POST | متابعة قناة إعلانات | `{webhook_channel_id}` | معلومات المتابعة | Bot |

---

## 🎵 **Soundboard APIs (لوحة الأصوات)**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/soundboard-sounds` | GET | الأصوات المتاحة | `Authorization: Bearer <token>` | قائمة الأصوات | User |
| `/guilds/{guild.id}/soundboard-sounds` | GET | أصوات السيرفر | `Authorization: Bot <token>` | قائمة الأصوات | Bot |
| `/soundboard-sounds/default` | GET | الأصوات الافتراضية | `Authorization: Bearer <token>` | قائمة الأصوات | User |

---

## 💬 **Forum APIs (المنتديات)**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/channels/{channel.id}/threads/forums` | POST | إنشاء منشور في المنتدى | `{name, message, tags}` | معلومات الموضوع | Both |
| `/channels/{channel.id}/tags` | GET | وسوم المنتدى | `Authorization: Bot <token>` | قائمة الوسوم | Both |
| `/channels/{channel.id}/tags` | POST | إنشاء وسم | `{name, emoji_id, moderated}` | معلومات الوسم الجديد | Bot |
| `/channels/{channel.id}/tags/{tag.id}` | PATCH | تحديث وسم | `{name, emoji_id, moderated}` | معلومات الوسم المحدث | Bot |
| `/channels/{channel.id}/tags/{tag.id}` | DELETE | حذف وسم | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🛡️ **Safety & Analytics APIs (الأمان والتحليلات)**

### **الأمان والمراقبة**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/guilds/{guild.id}/audit-logs` | GET | سجلات التدقيق | `Authorization: Bot <token>` | سجلات التدقيق | Bot |
| `/guilds/{guild.id}/vanity-url` | GET | رابط Vanity | `Authorization: Bot <token>` | `{code, uses}` | Bot |
| `/guilds/{guild.id}/widget` | GET | Widget السيرفر | `Authorization: Bot <token>` | معلومات Widget | Both |
| `/guilds/{guild.id}/widget.json` | GET | Widget بصيغة JSON | بدون توثيق | معلومات Widget | Public |
| `/guilds/{guild.id}/widget.png` | GET | Widget بصيغة صورة | `style=` | صورة Widget | Public |
| `/guilds/{guild.id}/welcome-screen` | GET | شاشة الترحيب | `Authorization: Bot <token>` | شاشة الترحيب | Both |
| `/guilds/{guild.id}/welcome-screen` | PATCH | تحديث شاشة الترحيب | `{enabled, welcome_channels}` | شاشة الترحيب المحدثة | Bot |

### **التحليلات**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/applications/{application.id}/analytics` | GET | تحليلات التطبيق | `Authorization: Bot <token>` | بيانات التحليلات | Bot |
| `/guilds/{guild.id}/analytics` | GET | تحليلات السيرفر | `Authorization: Bot <token>` | بيانات التحليلات | Bot |
| `/channels/{channel.id}/analytics` | GET | تحليلات القناة | `Authorization: Bot <token>` | بيانات التحليلات | Bot |

### **الوسائط والتفاعلات**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/channels/{channel.id}/attachments` | POST | رفع ملف | `files[]` | `{attachments: [{id, filename, ...}]}` | Both |
| `/channels/{channel.id}/messages/{message.id}/reactions/{emoji}` | PUT | إضافة تفاعل | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/messages/{message.id}/reactions/{emoji}` | DELETE | حذف تفاعل | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/messages/{message.id}/reactions/{emoji}/@me` | DELETE | حذف تفاعلك | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/messages/{message.id}/reactions/{emoji}/{user.id}` | DELETE | حذف تفاعل مستخدم | `Authorization: Bot <token>` | `{}` | Bot |
| `/channels/{channel.id}/messages/{message.id}/reactions` | DELETE | حذف كل التفاعلات | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🎫 **Ticket APIs (نظام التذاكر)**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/channels/{channel.id}/tickets` | POST | إنشاء تذكرة | `{topic, user_id}` | معلومات التذكرة | Bot |
| `/channels/{channel.id}/tickets/{ticket.id}` | PATCH | تحديث التذكرة | `{status, assignees}` | معلومات التذكرة المحدثة | Bot |
| `/channels/{channel.id}/tickets/{ticket.id}/transcript` | GET | نسخة التذكرة | `Authorization: Bot <token>` | نسخة المحادثة | Bot |

---

## ⚙️ **Application APIs (التطبيقات)**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/applications/{application.id}` | GET | معلومات التطبيق | `Authorization: Bot <token>` | معلومات التطبيق | Bot |
| `/applications/{application.id}` | PATCH | تحديث التطبيق | `{name, description, icon}` | معلومات التطبيق المحدث | Bot |
| `/applications/{application.id}/bot` | GET | معلومات بوت التطبيق | `Authorization: Bot <token>` | معلومات البوت | Bot |
| `/applications/{application.id}/assets` | GET | أصول التطبيق | `Authorization: Bot <token>` | قائمة الأصول | Bot |
| `/oauth2/applications/{application.id}` | GET | معلومات OAuth2 | `Authorization: Bot <token>` | معلومات OAuth2 | Bot |
| `/applications/{application.id}/role-connections/metadata` | GET | بيانات ربط الرتب | `Authorization: Bot <token>` | بيانات الربط | Bot |
| `/users/@me/applications/{application.id}/role-connection` | PUT | تحديث ربط رتب المستخدم | `{platform_name, metadata}` | بيانات الربط المحدثة | User |
| `/applications/{application.id}/entitlements` | POST | إنشاء ترخيص | `{user_id, sku_id}` | معلومات الترخيص | Bot |

### **ميزات السيرفر المتقدمة**
| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/guilds/{guild.id}/templates` | GET | قوالب السيرفر | `Authorization: Bot <token>` | قائمة القوالب | Bot |
| `/guilds/{guild.id}/templates` | POST | إنشاء قالب | `{name, description}` | `{template_code}` | Bot |
| `/guilds/{guild.id}/mfa` | POST | تفعيل/تعطيل MFA | `{level}` | معلومات السيرفر المحدثة | Bot |
| `/guilds/{guild.id}/regions` | GET | المناطق المتاحة | `Authorization: Bot <token>` | قائمة المناطق | Bot |
| `/guilds/{guild.id}/integrations` | GET | التكاملات | `Authorization: Bot <token>` | قائمة التكاملات | Bot |
| `/guilds/{guild.id}/integrations/{integration.id}` | DELETE | حذف تكامل | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🔍 **Search APIs (البحث)**

| الواجهة | الطريقة | الوصف | البيانات المرسلة | الاستجابة | نوع المستخدم |
|---------|---------|-------|------------------|-----------|---------------|
| `/guilds/{guild.id}/messages/search` | GET | بحث في الرسائل | `{content, author_id, mentions, ...}` | نتائج البحث | Bot |
| `/channels/{channel.id}/messages/search` | GET | بحث في قناة | `{content, author_id, mentions, ...}` | نتائج البحث | Bot |

---

## 📌 **معلومات عامة**

### **مفاتيح التوثيق**
| نوع المستخدم | مثال التوثيق | الوصف |
|--------------|-------------|-------|
| **User** | `Authorization: Bearer <oauth_token>` | توكن OAuth2 للمستخدم |
| **Bot** | `Authorization: Bot <bot_token>` | توكن البوت |
| **Webhook** | لا يحتاج | يستخدم `webhook.token` |

### **رموز الحالة (Status Codes)**
| الرمز | الوصف |
|-------|-------|
| `200` | نجاح (OK) |
| `201` | تم الإنشاء (Created) |
| `204` | نجاح بدون محتوى (No Content) |
| `400` | طلب خاطئ (Bad Request) |
| `401` | غير مصرح (Unauthorized) |
| `403` | محظور (Forbidden) |
| `404` | غير موجود (Not Found) |
| `429` | تجاوز الحد الأقصى للطلبات (Too Many Requests) |
| `500` | خطأ داخلي في الخادم (Internal Server Error) |

### **متطلبات خاصة**
| الميزة | المتطلبات |
|--------|-----------|
| هايبر سكواد | تطبيق معتمد من Discord |
| الملصقات (Stickers) | مستوى تعزيز 1 أو 2 للسيرفر |
| المنتديات (Forums) | مجتمع معتمد |
| التحليلات (Analytics) | Bot مع صلاحيات إدارية |
| الأنشطة (Activities) | تطبيق مع نشاط معتمد |
| Soundboard | حساب Discord Nitro |

### **حدود الاستخدام (Rate Limits)**
- تختلف حدود الاستخدام حسب نوع الـ API
- معظم الـ APIs لها حد 50 طلب/ثانية
- بعض الـ APIs الحساسة لها حدود أقل
- يتم إرجاع الحدود في رأس الاستجابة `X-RateLimit-*`

### **تنسيقات البيانات**
- **الطلب**: JSON لـ POST/PATCH/PUT
- **الاستجابة**: JSON دائمًا
- **الملفات**: multipart/form-data لرفع الملفات
- **التواريخ**: تنسيق ISO 8601

### **نصائح مهمة**
1. استخدم التوكن المناسب لنوع المستخدم
2. تحقق من الصلاحيات قبل استخدام الـ API
3. تعامل مع حدود الاستخدام بشكل صحيح
4. استخدم WebSocket للأحداث في الوقت الحقيقي
5. احفظ التوكن بأمان ولا تشاركه

---

## 📚 **المراجع والروابط**
- [Discord Developer Portal](https://discord.com/developers/docs)
- [Discord API Documentation](https://discord.com/developers/docs/reference)
- [Discord API Server](https://discord.gg/discord-developers)
- [Discord OAuth2 Documentation](https://discord.com/developers/docs/topics/oauth2)

---

**📅 تاريخ التحديث: ديسمبر 2025**  
**🔄 الإصدار: 1.0.0**  
**📝 بواسطة: مساعد Discord API**
---
**Searched  by github/iimazin11**
