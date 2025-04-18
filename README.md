# ✈️ Automated Flight Delay Data Pipeline — Powered by AWS 🚀

Welcome to the Flight Delay Data Pipeline! This serverless, event-driven architecture automatically processes flight data uploaded to S3, extracts delayed flights (🕐 > 60 mins), and loads it into Amazon Redshift for fast querying — all while keeping you notified with real-time SNS alerts. 💡📊

---

## 🧰 Tech Stack

| 🛠️ Service         | 🔍 Purpose                                      |
|--------------------|------------------------------------------------|
| ☁️ **Amazon S3**        | Store raw flight data files                   |
| 🕹️ **EventBridge**     | Detect new uploads & trigger Step Function    |
| 🔄 **Step Functions**   | Orchestrate Glue jobs & monitor flow         |
| 🔬 **Glue Crawler**     | Catalog schema of new datasets               |
| ⚗️ **Glue Job**         | Transform & filter flights with high delay   |
| 🧱 **Amazon Redshift**  | Load processed data for analytics            |
| 📢 **Amazon SNS**       | Notify via email on pipeline failure         |

---

## ⚙️ How It Works

1. 📥 **Upload** your flight dataset to the S3 bucket.
2. 🔔 **EventBridge** detects the file and triggers a **Step Function**.
3. 🧪 **Glue Crawler** catalogs the dataset and infers the schema.
4. 🧬 **Glue Job** filters only records where delay > 60 minutes.
5. 📊 **Redshift** stores final clean data in a table `flights_delayed_over_60`.
6. ⚠️ **SNS** sends alerts on failure (configurable via email/SMS).

---

## 🖼️ Architecture Diagram

[![View Architecture](https://drive.google.com/uc?export=view&id=15zbsMP3Wvfs_tFCLU-ozHAC4pahPP6xn)](https://drive.google.com/file/d/15zbsMP3Wvfs_tFCLU-ozHAC4pahPP6xn/view?usp=sharing)

---

## 📦 Output Example

The final Redshift table includes:
- ✈️ Flight ID
- 🏙️ Origin & Destination
- ⏰ Delay Duration
- 📆 Date & Time
- 🛫 Airline Carrier

---

## 🔐 IAM Policy Required

Ensure the Step Function execution role includes:
```json
{
  "Effect": "Allow",
  "Action": [
    "glue:*",
    "sns:*",
    "s3:GetObject",
    "redshift:*"
  ],
  "Resource": "*"
}
