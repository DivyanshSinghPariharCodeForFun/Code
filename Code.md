mongosh -u restrict_user -p '<password>' --authenticationDatabase restrict_app


use restrict_app

db.Applicationlogs.deleteMany({})
db.Audits.deleteMany({})
db.Changelogs.deleteMany({})
db.Completedreviews.deleteMany({})
db.Employeelogs.deleteMany({})
db.Employees.deleteMany({})
db.Frequency.deleteMany({})
db.Frequencylogs.deleteMany({})
db.Users.deleteMany({})
db.OldAdminNoRights.deleteMany({})
db.Session.deleteMany({})




To export collections in **CSV**, use `mongoexport` with `--type=csv` and `--fields`.

You **must explicitly specify the fields** for CSV export.

### General syntax:

```bash
mongoexport --db=restrict_app --collection=<collection> \
  --type=csv --fields=<comma-separated-fields> \
  --out=<filename>.csv \
  --username=restrict_user --authenticationDatabase=restrict_app
```

---

### Example (assuming basic fields):

```bash
mongoexport --db=restrict_app --collection=Users \
  --type=csv --fields=_id,email,username,role \
  --out=Users.csv \
  --username=restrict_user --authenticationDatabase=restrict_app
```

You must adjust `--fields` per collection.

---

### To get the field list quickly:

Run this inside Mongo CLI:

```js
db.Users.findOne()
```

Copy the keys and use them in `--fields`.

---

If you don't specify fields, you'll get:

```
error: export type csv requires --fields flag
```

There’s no auto-inference for fields in CSV mode. JSON exports are simpler for dynamic data.
