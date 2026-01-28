# 🎰 FLAGOUT - Free Fire Spinner CLI

> Automatic Free Fire gacha spinner with beautiful output, rare item tracking, and Telegram notifications

---

## ✨ Features

- 🤖 **Fully Automatic** - No user input required, processes all files with all payloads
- 🎨 **Beautiful Output** - Premium-styled console display with colors and emojis
- 🎁 **Rare Item Tracking** - Automatically saves accounts that find rare items
- 📱 **Telegram Notifications** - Instant notifications when rare items are found
- 🔒 **Secure** - Credentials stored in .env file
- 📊 **Progress Tracking** - Real-time progress for files and payloads
- ✅ **Auto-Marking** - Marks processed files to avoid duplicates

---

## 📋 Requirements

- Python 3.7+
- Internet connection
- Telegram bot (optional, for notifications)

---

## 🚀 Quick Start

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Setup Telegram (Optional)

Create a `.env` file:
```env
TELEGRAM_BOT_TOKEN=your_bot_token_here
TELEGRAM_ADMIN_ID=your_admin_id_here
```

### 3. Add Payloads

Run the script once and select option 2 to add payloads, or manually edit `payloads.json`:
```json
{
  "Payload Name": "hex_string_here"
}
```

### 4. Add Account Files

Create `.txt` or `.json` files with accounts:

**JSON format:**
```json
[
  {
    "uid": "1234567890",
    "password": "PASSWORD_HERE"
  }
]
```

**TXT format:**
```
1234567890|PASSWORD_HERE
1234567891|PASSWORD_HERE
```

### 5. Run

```bash
python app.py
```

**That's it!** The script will automatically process everything.

---

## 📁 File Structure

```
📁 Project/
  ├── app.py                    # Main script
  ├── requirements.txt          # Dependencies
  ├── .env                      # Telegram credentials (create this)
  ├── payloads.json            # Gacha payloads
  ├── item_map.json            # Rare items to track
  ├── data.json                # All items database
  ├── rearfound.json           # Accounts with rare items
  ├── accounts_part1.json      # Your account files
  ├── my_pb2.py                # Protobuf files
  ├── output_pb2.py            # (required)
  ├── MajorLoginRes_pb2.py     # (required)
  └── FOUND_ITEMS/             # Detailed logs
      └── found_accounts.json
```

---

## 🎯 How It Works

### Automatic Processing Flow

```
1. Script starts
   ↓
2. Finds all account files (.txt, .json)
   ↓
3. Loads all payloads
   ↓
4. For each payload:
   ├─ Process all account files
   ├─ Show beautiful output
   ├─ Save rare accounts
   └─ Send to Telegram
   ↓
5. Mark files as processed (✅)
   ↓
6. Complete!
```

---

## 📊 Output Example

```
🤖 AUTO MODE ACTIVATED
Processing all account files with all payloads...

📁 Found 1 account file(s)
🎯 Found 4 payload(s)
────────────────────────────────────────────────────────────


🎰 PAYLOAD 1/4: Gojo Bundle
============================================================

📂 File 1/1: accounts_part1.json (100 accounts)
────────────────────────────────────────────────────────────

────────────────────────────────────────
🎰 SUCCESS ACCOUNT
👤 Username  : ꜱꫝᴇᴇDx⁰⁶⁷
🆔 Account ID : 13226423931
🎁 Item Found : Satoru Gojo Bundle
   ⭐ RARE ITEM ACCOUNT SAVED TO rearfound.json!
   ✅ File sent to Telegram successfully!
────────────────────────────────────────

✅ File Complete: Success: 85 | Failed: 15 | Items: 3
────────────────────────────────────────────────────────────


============================================================
🎉 ALL PROCESSING COMPLETE!
============================================================
```

---

## 🎁 Rare Item Tracking

### Setup

Edit `item_map.json` with items you want to track:
```json
{
  "203052003": "CLOTH: Satoru Gojo Top",
  "710052004": "Satoru Gojo Bundle",
  "907105202": "Fist - Divergent Fist"
}
```

### What Happens

When an account finds a rare item:
1. ✅ Account saved to `rearfound.json`
2. ✅ File sent to Telegram (if configured)
3. ✅ Detailed log saved to `FOUND_ITEMS/`

### rearfound.json Format

```json
[
  {
    "uid": "4151814546",
    "password": "ACCOUNT_PASSWORD",
    "accountId": "13226423931",
    "accountNickname": "ꜱꫝᴇᴇDx⁰⁶⁷"
  }
]
```

---

## 📱 Telegram Integration

### Setup

1. Create a Telegram bot with [@BotFather](https://t.me/BotFather)
2. Get your bot token
3. Get your admin ID (use [@userinfobot](https://t.me/userinfobot))
4. Create `.env` file:

```env
TELEGRAM_BOT_TOKEN=8030491906:AAElLmgkUCwNHrl-HN691lAgFAq_BWkExJI
TELEGRAM_ADMIN_ID=6218146252
```

### What You Get

When rare items are found, you'll receive:
- 📁 `rearfound.json` file
- 📝 Timestamp
- 🎯 Instant notification

---

## ⚙️ Configuration

### Payloads

Add via menu (option 2) or edit `payloads.json`:
```json
{
  "Gojo Bundle": "0a1a0801100118022001",
  "JJK - Fist": "0a1a0801100118022002"
}
```

### Item Mapping

Edit `item_map.json` for rare items:
```json
{
  "ITEM_ID": "Item Name"
}
```

### Data File

`data.json` contains all 31,785+ items for name resolution.

---

## 🔧 Advanced Usage

### Manual Mode

To switch back to manual mode, edit `app.py` line ~717:

```python
# Change:
asyncio.run(auto_mode())

# To:
asyncio.run(main_menu())
```

### Reprocess Files

Remove ✅ from filename:
```
accounts_part1 ✅.json  →  accounts_part1.json
```

---

## 📖 Documentation

- **AUTO_MODE.md** - Automatic mode guide
- **INDEX.md** - Documentation navigation (if exists)

---

## 🛠️ Troubleshooting

### No Account Files Found
- Ensure files are `.txt` or `.json`
- Check they're in the same directory as `app.py`
- Verify they're not in the exclude list

### No Payloads Found
- Add payloads via menu option 2
- Or manually edit `payloads.json`

### Telegram Not Working
- Check `.env` file exists
- Verify bot token is correct
- Verify admin ID is correct
- Send `/start` to your bot first

### Import Errors
- Run `pip install -r requirements.txt`
- Ensure all `.pb2.py` files are present

---

## 📊 Statistics

- **Items Database**: 31,785+ items
- **Supported Formats**: JSON, TXT
- **Platforms**: Windows, Linux, macOS
- **Python**: 3.7+

---

## 🔒 Security

- ✅ Credentials in `.env` file
- ✅ `.gitignore` protects sensitive files
- ✅ Passwords not displayed in output
- ✅ Secure credential storage

---

## 📝 License

Free to use and modify for personal use.

---

## 👨‍💻 Credits

**Created by:** TSun-Studio & Saeedxdie  
**Original Base:** Flexbase & Spideerio  
**Enhanced Features:** Auto Mode, Beautiful Output, Telegram Integration, Rare Item Tracking

---

## 🎉 Quick Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Run automatic mode
python app.py

# That's it!
```

---

**Enjoy automatic gacha spinning with beautiful output and Telegram notifications!** 🎰🎉
