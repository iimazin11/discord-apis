# 📚 Discord APIs Documentation - Comprehensive Guide

## 📋 Table of Contents
1. [🔐 Authentication APIs](#-authentication-apis)
2. [👤 User APIs](#-user-apis)
3. [🤖 Bot APIs](#-bot-apis)
4. [🎮 Game & Hyper Squad APIs](#-game--hyper-squad-apis)
5. [🏷️ Sticker APIs](#️-sticker-apis)
6. [👥 Thread APIs](#-thread-apis)
7. [🎭 Stage Discovery APIs](#-stage-discovery-apis)
8. [📢 Announcement APIs](#-announcement-apis)
9. [🎵 Soundboard APIs](#-soundboard-apis)
10. [💬 Forum APIs](#-forum-apis)
11. [🛡️ Safety & Analytics APIs](#️-safety--analytics-apis)
12. [🎫 Ticket APIs](#-ticket-apis)
13. [⚙️ Application APIs](#️-application-apis)
14. [🔍 Search APIs](#-search-apis)
15. [📌 General Information](#-general-information)

---

## 🔐 **Authentication APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/oauth2/authorize` | GET | OAuth2 Authorization | `client_id`, `redirect_uri`, `scope`, `response_type` | Authorization Page | User |
| `/oauth2/token` | POST | Get Token | `client_id`, `client_secret`, `grant_type`, `code`, `redirect_uri` | `{access_token, refresh_token, expires_in}` | User |
| `/oauth2/token/revoke` | POST | Revoke Token | `client_id`, `client_secret`, `token` | `{}` | User |
| `/oauth2/@me` | GET | Current User Information | `Authorization: Bearer <token>` | User Information | User |

---

## 👤 **User APIs**

### **User Information**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/users/@me` | GET | Get Profile Data | `Authorization: Bearer <token>` | Complete User Information | User |
| `/users/@me` | PATCH | Update User Data | `{username, avatar, bio, ...}` | Updated User Information | User |
| `/users/@me/connections` | GET | Connected Accounts | `Authorization: Bearer <token>` | List of Connected Accounts | User |
| `/users/@me/guilds` | GET | Joined Servers | `Authorization: Bearer <token>` | List of Servers | User |
| `/users/@me/billing` | GET | Billing Information | `Authorization: Bearer <token>` | Subscription Information | User |
| `/users/@me/affinities/users` | GET | Close Users | `Authorization: Bearer <token>` | List of Close Users | User |

### **Direct Messages**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/users/@me/channels` | GET | Get DM Channels | `Authorization: Bearer <token>` | List of Channels | User |
| `/users/@me/channels` | POST | Create DM | `{recipient_id}` | New Channel Information | User |
| `/channels/{channel.id}/messages` | GET | Get Messages | `Authorization: Bearer <token>` | List of Messages | User |
| `/channels/{channel.id}/messages` | POST | Send Message | `{content, embeds, components}` | Sent Message | User |
| `/channels/{channel.id}/messages/{message.id}` | PUT | Edit Message | `{content, embeds, components}` | Edited Message | User |
| `/channels/{channel.id}/messages/{message.id}` | DELETE | Delete Message | `Authorization: Bearer <token>` | `{}` | User |

---

## 🤖 **Bot APIs**

### **Main Bot APIs**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/gateway` | GET | WebSocket Gateway | `Authorization: Bot <token>` | `{url, shards}` | Bot |
| `/gateway/bot` | GET | Bot Gateway Information | `Authorization: Bot <token>` | `{url, shards, session_start_limit}` | Bot |

### **Guilds**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/guilds/{guild.id}` | GET | Server Information | `Authorization: Bot <token>` | Server Information | Bot |
| `/guilds/{guild.id}` | PATCH | Update Server | `{name, icon, region, ...}` | Updated Server Information | Bot |
| `/guilds/{guild.id}` | DELETE | Delete Server | `Authorization: Bot <token>` | `{}` | Bot |
| `/guilds/{guild.id}/channels` | GET | Server Channels | `Authorization: Bot <token>` | List of Channels | Bot |
| `/guilds/{guild.id}/channels` | POST | Create Channel | `{name, type, topic, ...}` | New Channel Information | Bot |
| `/guilds/{guild.id}/members` | GET | Server Members | `Authorization: Bot <token>` | List of Members | Bot |
| `/guilds/{guild.id}/members/{user.id}` | GET | Member Information | `Authorization: Bot <token>` | Member Information | Bot |
| `/guilds/{guild.id}/members/{user.id}` | PUT | Edit Member | `{nick, roles, mute, deaf}` | Updated Member Information | Bot |
| `/guilds/{guild.id}/members/{user.id}` | DELETE | Kick Member | `Authorization: Bot <token>` | `{}` | Bot |
| `/guilds/{guild.id}/bans` | GET | Banned Users | `Authorization: Bot <token>` | List of Bans | Bot |
| `/guilds/{guild.id}/bans/{user.id}` | PUT | Ban User | `{delete_message_days, reason}` | `{}` | Bot |
| `/guilds/{guild.id}/bans/{user.id}` | DELETE | Unban User | `Authorization: Bot <token>` | `{}` | Bot |
| `/guilds/{guild.id}/roles` | GET | Server Roles | `Authorization: Bot <token>` | List of Roles | Bot |
| `/guilds/{guild.id}/roles` | POST | Create Role | `{name, permissions, color, ...}` | New Role Information | Bot |
| `/guilds/{guild.id}/roles/{role.id}` | PATCH | Edit Role | `{name, permissions, color, ...}` | Updated Role Information | Bot |
| `/guilds/{guild.id}/roles/{role.id}` | DELETE | Delete Role | `Authorization: Bot <token>` | `{}` | Bot |

### **Channels**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/channels/{channel.id}` | GET | Channel Information | `Authorization: Bot <token>` | Channel Information | Both |
| `/channels/{channel.id}` | PATCH | Edit Channel | `{name, topic, position, ...}` | Updated Channel Information | Bot |
| `/channels/{channel.id}` | DELETE | Delete Channel | `Authorization: Bot <token>` | `{}` | Bot |
| `/channels/{channel.id}/messages` | GET | Get Messages | `Authorization: Bot <token>` | List of Messages | Both |
| `/channels/{channel.id}/messages` | POST | Send Message | `{content, embeds, components, tts}` | Sent Message | Both |
| `/channels/{channel.id}/messages/{message.id}` | GET | Get Specific Message | `Authorization: Bot <token>` | Message Content | Both |
| `/channels/{channel.id}/messages/{message.id}` | PATCH | Edit Message | `{content, embeds, components}` | Edited Message | Both |
| `/channels/{channel.id}/messages/{message.id}` | DELETE | Delete Message | `Authorization: Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/messages/bulk-delete` | POST | Bulk Delete | `{messages: [id1, id2, ...]}` | `{}` | Bot |
| `/channels/{channel.id}/permissions/{overwrite.id}` | PUT | Edit Permissions | `{allow, deny, type}` | `{}` | Bot |
| `/channels/{channel.id}/permissions/{overwrite.id}` | DELETE | Remove Permissions | `Authorization: Bot <token>` | `{}` | Bot |
| `/channels/{channel.id}/typing` | POST | Typing Indicator | `Authorization: Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/pins` | GET | Pinned Messages | `Authorization: Bot <token>` | List of Pinned Messages | Both |
| `/channels/{channel.id}/pins/{message.id}` | PUT | Pin Message | `Authorization: Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/pins/{message.id}` | DELETE | Unpin Message | `Authorization: Bot <token>` | `{}` | Both |

### **Interactions**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/interactions/{interaction.id}/{interaction.token}/callback` | POST | Respond to Interaction | `{type, data}` | `{}` | Bot |
| `/webhooks/{application.id}/{interaction.token}/messages/@original` | GET | Get Original Response | `Authorization: Bot <token>` | Message Content | Bot |
| `/webhooks/{application.id}/{interaction.token}/messages/@original` | PATCH | Edit Original Response | `{content, embeds, components}` | Edited Message | Bot |
| `/webhooks/{application.id}/{interaction.token}/messages/@original` | DELETE | Delete Original Response | `Authorization: Bot <token>` | `{}` | Bot |
| `/webhooks/{application.id}/{interaction.token}` | POST | Create Follow-up Response | `{content, embeds, components}` | New Message | Bot |

### **Webhooks**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/webhooks/{webhook.id}` | GET | Webhook Information | `Authorization: Bot <token>` | Webhook Information | Bot |
| `/webhooks/{webhook.id}` | PATCH | Edit Webhook | `{name, avatar, channel_id}` | Updated Webhook Information | Bot |
| `/webhooks/{webhook.id}` | DELETE | Delete Webhook | `Authorization: Bot <token>` | `{}` | Bot |
| `/webhooks/{webhook.id}/{webhook.token}` | POST | Send via Webhook | `{content, embeds, username, avatar_url}` | `{}` | Both |
| `/webhooks/{webhook.id}/{webhook.token}/messages/{message.id}` | PATCH | Edit Webhook Message | `{content, embeds}` | Edited Message | Bot |
| `/webhooks/{webhook.id}/{webhook.token}/messages/{message.id}` | DELETE | Delete Webhook Message | `Authorization: Bot <token>` | `{}` | Bot |

### **Application Commands**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/applications/{application.id}/commands` | GET | Get Global Commands | `Authorization: Bot <token>` | List of Commands | Bot |
| `/applications/{application.id}/commands` | POST | Create Global Command | `{name, description, options}` | New Command Information | Bot |
| `/applications/{application.id}/guilds/{guild.id}/commands` | GET | Get Server Commands | `Authorization: Bot <token>` | List of Commands | Bot |
| `/applications/{application.id}/guilds/{guild.id}/commands` | POST | Create Server Command | `{name, description, options}` | New Command Information | Bot |
| `/applications/{application.id}/guilds/{guild.id}/commands/{command.id}` | PATCH | Edit Command | `{name, description, options}` | Updated Command Information | Bot |
| `/applications/{application.id}/guilds/{guild.id}/commands/{command.id}` | DELETE | Delete Command | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🎮 **Game & Hyper Squad APIs**

### **Hyper Squad**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/activities` | GET | Available Activities | `Authorization: Bearer/Bot <token>` | List of Activities | Both |
| `/activities/{activity.id}/sessions` | POST | Start Activity | `{max_age, max_uses, target_application_id}` | Session Information | Both |
| `/channels/{channel.id}/invites` | POST | Activity Invitation | `{target_type, target_application_id}` | Invitation Link | Both |
| `/applications/{application.id}/entitlements` | GET | Application Entitlements | `Authorization: Bot <token>` | List of Entitlements | Bot |
| `/store/skus` | GET | Store Products | `Authorization: Bearer <token>` | List of Products | User |
| `/store/published-listings/skus/{sku.id}` | GET | Product Details | `Authorization: Bearer <token>` | Product Details | User |
| `/store/skus/{sku.id}/purchase` | POST | Purchase Product | `Authorization: Bearer <token>` | `{gift_code, gift_url}` | User |

### **Games**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/users/@me/games` | GET | User Games | `Authorization: Bearer <token>` | List of Games | User |
| `/applications/{application.id}/store-listing` | GET | Store Page | `Authorization: Bearer <token>` | Store Information | User |
| `/applications/{application.id}/achievements` | GET | Game Achievements | `Authorization: Bot <token>` | List of Achievements | Bot |
| `/users/@me/applications/{application.id}/achievements` | GET | User Achievements | `Authorization: Bearer <token>` | User Achievements | User |
| `/applications/{application.id}/entitlements/gifts` | POST | Create Gift | `Authorization: Bot <token>` | `{gift_code}` | Bot |

### **Voice Activities**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/channels/{channel.id}/voice-status` | GET | Voice Status | `Authorization: Bearer <token>` | Voice Information | User |
| `/channels/{channel.id}/voice-status/@me` | PUT | Update Voice Status | `{status}` | `{}` | User |
| `/applications/{application.id}/voice-states` | POST | Update Application Voice State | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🏷️ **Sticker APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/stickers/{sticker.id}` | GET | Sticker Information | `Authorization: Bot <token>` | Sticker Information | Both |
| `/guilds/{guild.id}/stickers` | GET | Server Stickers | `Authorization: Bot <token>` | List of Stickers | Both |
| `/guilds/{guild.id}/stickers/{sticker.id}` | GET | Specific Sticker | `Authorization: Bot <token>` | Sticker Information | Both |
| `/guilds/{guild.id}/stickers` | POST | Create Sticker | `files[], {name, description, tags}` | New Sticker Information | Bot |
| `/guilds/{guild.id}/stickers/{sticker.id}` | PATCH | Update Sticker | `{name, description, tags}` | Updated Sticker Information | Bot |
| `/guilds/{guild.id}/stickers/{sticker.id}` | DELETE | Delete Sticker | `Authorization: Bot <token>` | `{}` | Bot |
| `/sticker-packs` | GET | Sticker Packs | `Authorization: Bearer <token>` | List of Packs | User |

---

## 👥 **Thread APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/channels/{channel.id}/threads` | POST | Create Thread | `{name, auto_archive_duration, type}` | Thread Information | Both |
| `/channels/{channel.id}/threads` | GET | Active Threads | `Authorization: Bot <token>` | List of Threads | Both |
| `/channels/{channel.id}/threads/archived/public` | GET | Public Archived Threads | `Authorization: Bot <token>` | List of Threads | Both |
| `/channels/{channel.id}/threads/archived/private` | GET | Private Archived Threads | `Authorization: Bot <token>` | List of Threads | Both |
| `/channels/{channel.id}/users/@me/threads/archived/private` | GET | Your Archived Threads | `Authorization: Bearer <token>` | List of Threads | User |
| `/channels/{thread.id}/messages` | GET | Thread Messages | `Authorization: Bot <token>` | List of Messages | Both |
| `/channels/{thread.id}/members` | GET | Thread Members | `Authorization: Bot <token>` | List of Members | Both |
| `/channels/{thread.id}/members/@me` | PUT | Join Thread | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{thread.id}/members/{user.id}` | PUT | Add Member to Thread | `Authorization: Bot <token>` | `{}` | Bot |
| `/channels/{thread.id}/members/@me` | DELETE | Leave Thread | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{thread.id}/members/{user.id}` | DELETE | Remove Member from Thread | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🎭 **Stage Discovery APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/stage-instances` | POST | Create Stage | `{channel_id, topic, privacy_level}` | Stage Information | Bot |
| `/stage-instances/{channel.id}` | GET | Stage Information | `Authorization: Bot <token>` | Stage Information | Bot |
| `/stage-instances/{channel.id}` | PATCH | Update Stage | `{topic, privacy_level}` | Updated Stage Information | Bot |
| `/stage-instances/{channel.id}` | DELETE | Delete Stage | `Authorization: Bot <token>` | `{}` | Bot |

---

## 📢 **Announcement Channels APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/channels/{channel.id}/messages/{message.id}/crosspost` | POST | Crosspost Announcement | `Authorization: Bot <token>` | Crossposted Message | Bot |
| `/channels/{channel.id}/followers` | POST | Follow Announcement Channel | `{webhook_channel_id}` | Follow Information | Bot |

---

## 🎵 **Soundboard APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/soundboard-sounds` | GET | Available Sounds | `Authorization: Bearer <token>` | List of Sounds | User |
| `/guilds/{guild.id}/soundboard-sounds` | GET | Server Sounds | `Authorization: Bot <token>` | List of Sounds | Bot |
| `/soundboard-sounds/default` | GET | Default Sounds | `Authorization: Bearer <token>` | List of Sounds | User |

---

## 💬 **Forum APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/channels/{channel.id}/threads/forums` | POST | Create Forum Post | `{name, message, tags}` | Thread Information | Both |
| `/channels/{channel.id}/tags` | GET | Forum Tags | `Authorization: Bot <token>` | List of Tags | Both |
| `/channels/{channel.id}/tags` | POST | Create Tag | `{name, emoji_id, moderated}` | New Tag Information | Bot |
| `/channels/{channel.id}/tags/{tag.id}` | PATCH | Update Tag | `{name, emoji_id, moderated}` | Updated Tag Information | Bot |
| `/channels/{channel.id}/tags/{tag.id}` | DELETE | Delete Tag | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🛡️ **Safety & Analytics APIs**

### **Security & Monitoring**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/guilds/{guild.id}/audit-logs` | GET | Audit Logs | `Authorization: Bot <token>` | Audit Logs | Bot |
| `/guilds/{guild.id}/vanity-url` | GET | Vanity URL | `Authorization: Bot <token>` | `{code, uses}` | Bot |
| `/guilds/{guild.id}/widget` | GET | Server Widget | `Authorization: Bot <token>` | Widget Information | Both |
| `/guilds/{guild.id}/widget.json` | GET | Widget JSON | No Authentication | Widget Information | Public |
| `/guilds/{guild.id}/widget.png` | GET | Widget Image | `style=` | Widget Image | Public |
| `/guilds/{guild.id}/welcome-screen` | GET | Welcome Screen | `Authorization: Bot <token>` | Welcome Screen | Both |
| `/guilds/{guild.id}/welcome-screen` | PATCH | Update Welcome Screen | `{enabled, welcome_channels}` | Updated Welcome Screen | Bot |

### **Analytics**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/applications/{application.id}/analytics` | GET | Application Analytics | `Authorization: Bot <token>` | Analytics Data | Bot |
| `/guilds/{guild.id}/analytics` | GET | Server Analytics | `Authorization: Bot <token>` | Analytics Data | Bot |
| `/channels/{channel.id}/analytics` | GET | Channel Analytics | `Authorization: Bot <token>` | Analytics Data | Bot |

### **Media & Reactions**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/channels/{channel.id}/attachments` | POST | Upload File | `files[]` | `{attachments: [{id, filename, ...}]}` | Both |
| `/channels/{channel.id}/messages/{message.id}/reactions/{emoji}` | PUT | Add Reaction | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/messages/{message.id}/reactions/{emoji}` | DELETE | Remove Reaction | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/messages/{message.id}/reactions/{emoji}/@me` | DELETE | Remove Your Reaction | `Authorization: Bearer/Bot <token>` | `{}` | Both |
| `/channels/{channel.id}/messages/{message.id}/reactions/{emoji}/{user.id}` | DELETE | Remove User Reaction | `Authorization: Bot <token>` | `{}` | Bot |
| `/channels/{channel.id}/messages/{message.id}/reactions` | DELETE | Remove All Reactions | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🎫 **Ticket APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/channels/{channel.id}/tickets` | POST | Create Ticket | `{topic, user_id}` | Ticket Information | Bot |
| `/channels/{channel.id}/tickets/{ticket.id}` | PATCH | Update Ticket | `{status, assignees}` | Updated Ticket Information | Bot |
| `/channels/{channel.id}/tickets/{ticket.id}/transcript` | GET | Ticket Transcript | `Authorization: Bot <token>` | Conversation Transcript | Bot |

---

## ⚙️ **Application APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/applications/{application.id}` | GET | Application Information | `Authorization: Bot <token>` | Application Information | Bot |
| `/applications/{application.id}` | PATCH | Update Application | `{name, description, icon}` | Updated Application Information | Bot |
| `/applications/{application.id}/bot` | GET | Application Bot Information | `Authorization: Bot <token>` | Bot Information | Bot |
| `/applications/{application.id}/assets` | GET | Application Assets | `Authorization: Bot <token>` | List of Assets | Bot |
| `/oauth2/applications/{application.id}` | GET | OAuth2 Information | `Authorization: Bot <token>` | OAuth2 Information | Bot |
| `/applications/{application.id}/role-connections/metadata` | GET | Role Connection Metadata | `Authorization: Bot <token>` | Connection Data | Bot |
| `/users/@me/applications/{application.id}/role-connection` | PUT | Update User Role Connection | `{platform_name, metadata}` | Updated Connection Data | User |
| `/applications/{application.id}/entitlements` | POST | Create Entitlement | `{user_id, sku_id}` | Entitlement Information | Bot |

### **Advanced Server Features**
| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/guilds/{guild.id}/templates` | GET | Server Templates | `Authorization: Bot <token>` | List of Templates | Bot |
| `/guilds/{guild.id}/templates` | POST | Create Template | `{name, description}` | `{template_code}` | Bot |
| `/guilds/{guild.id}/mfa` | POST | Enable/Disable MFA | `{level}` | Updated Server Information | Bot |
| `/guilds/{guild.id}/regions` | GET | Available Regions | `Authorization: Bot <token>` | List of Regions | Bot |
| `/guilds/{guild.id}/integrations` | GET | Integrations | `Authorization: Bot <token>` | List of Integrations | Bot |
| `/guilds/{guild.id}/integrations/{integration.id}` | DELETE | Delete Integration | `Authorization: Bot <token>` | `{}` | Bot |

---

## 🔍 **Search APIs**

| Endpoint | Method | Description | Data Sent | Response | User Type |
|----------|--------|-------------|-----------|----------|-----------|
| `/guilds/{guild.id}/messages/search` | GET | Search Messages in Server | `{content, author_id, mentions, ...}` | Search Results | Bot |
| `/channels/{channel.id}/messages/search` | GET | Search Messages in Channel | `{content, author_id, mentions, ...}` | Search Results | Bot |

---

## 📌 **General Information**

### **Authentication Keys**
| User Type | Authentication Example | Description |
|-----------|------------------------|-------------|
| **User** | `Authorization: Bearer <oauth_token>` | OAuth2 Token for Users |
| **Bot** | `Authorization: Bot <bot_token>` | Bot Token |
| **Webhook** | Not Required | Uses `webhook.token` |

### **Status Codes**
| Code | Description |
|------|-------------|
| `200` | OK (Success) |
| `201` | Created |
| `204` | No Content (Success without content) |
| `400` | Bad Request |
| `401` | Unauthorized |
| `403` | Forbidden |
| `404` | Not Found |
| `429` | Too Many Requests (Rate Limit) |
| `500` | Internal Server Error |

### **Special Requirements**
| Feature | Requirements |
|---------|--------------|
| Hyper Squad | Discord Approved Application |
| Stickers | Server Boost Level 1 or 2 |
| Forums | Verified Community |
| Analytics | Bot with Administrative Permissions |
| Activities | Application with Approved Activity |
| Soundboard | Discord Nitro Account |

### **Rate Limits**
- Rate limits vary by API type
- Most APIs have a limit of 50 requests/second
- Some sensitive APIs have lower limits
- Limits are returned in response headers `X-RateLimit-*`

### **Data Formats**
- **Request**: JSON for POST/PATCH/PUT
- **Response**: Always JSON
- **Files**: multipart/form-data for file uploads
- **Dates**: ISO 8601 format

### **Important Tips**
1. Use the appropriate token for user type
2. Check permissions before using API
3. Handle rate limits properly
4. Use WebSocket for real-time events
5. Store tokens securely and don't share them

---

## 📚 **References & Links**
- [Discord Developer Portal](https://discord.com/developers/docs)
- [Discord API Documentation](https://discord.com/developers/docs/reference)
- [Discord API Server](https://discord.gg/discord-developers)
- [Discord OAuth2 Documentation](https://discord.com/developers/docs/topics/oauth2)

---

**📅 Update Date: December 2025**  
**🔄 Version: 1.0.0**  
**📝 By: Discord API Assistant**
---
**Searched by github/iimazin11**
