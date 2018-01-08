## List all files in current and sub directories
```bash
$ find
.
./test3
./testdir
./testdir/test
./testdir/test1
./test2
./test
./test1
```

## Search specific directory or path
### find all
```bash
$ find ./testdir
./testdir
./testdir/test
./testdir/test1
```
### find by name
```bash
$ find ./testdir -name "test0*"
./testdir/test03
./testdir/test02
./testdir/test01
```

### find ignore the case 
```bash
$ find ./testdir -iname "test0*"
./testdir/TEST03
./testdir/test03
./testdir/test02
./testdir/test01
```

## Limit depth of directory traversal
```bash
$ find . -maxdepth 1 -name "test"
./test
$ find . -maxdepth 2 -name "test"
./testdir/test
./test
```

## Invert match
```bash
$ find . -not -name "test0*"
.
./test3
./testdir
./testdir/TEST03
./testdir/test
./testdir/test1
./test2
./test
./test1
```

## Combine multiple search criterias
### specifying name and inverting
```bash
$ find . -iname "test0*"
./testdir/TEST03
./testdir/test03
./testdir/test02
./testdir/test01
$ find . -iname "test0*" ! -name "TEST*"
./testdir/test03
./testdir/test02
./testdir/test01
```
### OR operator
```bash
$ find . -name "test0*"
./testdir/test03
./testdir/test02
./testdir/test01
$ find . -name "test0*" -o -name "TEST*"
./testdir/TEST03
./testdir/test03
./testdir/test02
./testdir/test01
```
## Search only files or only directories
```bash
$ find . -name "test*" -type f
./test3
./testdir/test03
./testdir/test
./testdir/test02
./testdir/test01
./testdir/test1
./test2
./test
./test1
$ find . -name "test*" -type d
./testdir
```

## Search multiple directories together
```bash
$ find ./ ../ -name test
./testdir/test
./test
../deviceinfo/testdir/test
../deviceinfo/test
../docker/test
```

## Find hidden files
```bash
$ find ~ -type f -name ".*"
```

## Find files with certain permissions
```bash
$ find . -type f -perm 0664
$ find . -type f ! -perm 0777
```
## Find files with sgid/suid bits set
## Find readonly files
## Find executable files
## Find files belonging to particular user
## Search files belonging to group
## Find files modified N days back
## Find files accessed in last N days
## Find files modified in a range of days
## Find files changed in last N minutes
## Files modified in last hour
## Find Accessed Files in Last 1 Hour
## Find files of given size
## Find files in a size range
## Find largest and smallest files
## Find empty files and directories
## List out the found files
## Delete all matching files or directories