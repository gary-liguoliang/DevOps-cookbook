# DevOps-cookbook

## Python

### String

**index**
```python
s = 'github.com/guoliang-dev'
s.index('g')  # 0 - firs index from left
s.rindex('g')  # 18 - firt index from right
s.index('g', s.index('g') + 1)  # 11 second index from left

# contains? 
try:
    s.index('python')
except ValueError as e:
    print 'cannot find the value: %s' % e
```

**adjust**
```python
s='github'
s.ljust(20, '-')  # 'github--------------'
s.rjust(20, '-')  # '--------------github'
```

### I/O

### Datetime



## Windows CMD

### I/O

**robocopy**
```bat
robocopy c:/tmp/sf c:/tmp/dest /MIR

```
return code: `1` - `One of more files were copied successfully.` [robocopy return codes](https://blogs.technet.microsoft.com/deploymentguys/2008/06/16/robocopy-exit-codes/)


### Windows Service

```bat
sc \\<remote-server> <service>
sc \\<remote-server> stop <service>
sc \\<remote-server> start <service>

net start <service>
net stop <service>
```
[*net start vs. sc start*](https://superuser.com/questions/315166/net-start-service-and-sc-start-what-is-the-difference)

### Windows Scheduler Job

### PsExec

### HPC



## Database

### SQL

### H2

### SQL Server / T-SQL

### MySQL



## PowerShell



## Bash



## Vim

