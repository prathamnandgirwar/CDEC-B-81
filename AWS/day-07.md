
# 📸 Backup Using Snapshots

---

## 📝 Manual Snapshot

1. Go to AWS Console → EC2
2. Click **Volumes**
3. Select Volume
4. Click **Actions → Create Snapshot**
5. Add Description
6. Click **Create Snapshot**

To view snapshots:
- EC2 → Snapshots

---

# 🔄 Automating Snapshot (Lifecycle Policy)

---

## Create Snapshot Policy

1. Go to **Amazon Data Lifecycle Manager (DLM)**
2. Click **Create lifecycle policy**
3. Select **EBS Snapshot policy**
4. Resource Type → Volume
5. Add Tag (Example: Environment=Production)
6. Define Schedule:
   - Frequency: Daily
   - Retention: 7 days
7. Review and Create

Now snapshots will be automatically created and deleted.

---

# 📌 Final Summary

✔ Backup Methods:
- Manual Snapshot
- Automated Lifecycle Policy

---
