# Data Version Control Example (DVC)
Source: [dvc.org](https://dvc.org/doc/start)

### Project Setup

#### Init Git
```bash
git init
```

#### Init DVC
```bash
dvc init

git status
git commit -m "Initialize DVC"
git push
```

#### Add some data to the project
```bash
mkdir data
# Add .csv file to data/
```

### Configuring a dvc remote storage

#### Add dvc data storage remote (Google Drive as example)
```bash
# copy ID of your folder drive.google.com/drive/folders/[ID]
# you will need to authenticate and allow dvc to access that folder
dvc remote add -d storage gdrive://[ID]

git commit .dvc/config -m "Configure remote storage"
git push
```

### Adding and pushing data to dvc remote storage

#### Add data to dvc
```bash
dvc add data/data.csv
# This .csv file will be automaticaly added to .gitignore
```

#### Push data to dvc
```bash
dvc push
```

#### Push changes to git
```bash
git add data/data.csv.dvc
git add data/.gitignore
git commit -m "Add raw data"
git push
```

### Pulling data from dvc storage
For example we remove our file.

```bash
rm -f data/data.csv
rm -rf .dvc/cache
```

Let's pull from dvc.

```bash
dvc pull
```

### Making local changes

```bash
mkdir tmp
cp data/data.csv tmp/data.csv
cat tmp/data.csv >> data/data.csv
ls -lh data
```

```bash
dvc add data/data.csv
git add data/data.csv.dvc
git commit -m "Dataset updates"
dvc push
```

### Restoring changes
Check changes:
```bash
git log --online
```

Restore changes:
```bash
# Make sure to checkout data/data.csv.dvc and not data/data.csv !
git checkout HEAD^1 data/data.csv.dvc
dvc checkout
```

Verify:
```bash
ls -lh data
```


