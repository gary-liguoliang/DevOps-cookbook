# DevOps-cookbook

## Python

### pip

```bash
# install pip with proxy and accept certificate
pip install pywinrm --proxy http://proxy.server:80 --trusted-host pypi.python.org
```


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

**count occurrences**
```python
s = 'cookbook'
s.count('o') # 4
s.count('o', 0, 2) # 1
```

### datetime
```python
>>> datetime.datetime.now().strftime('%Y%m%d_%H%M%S')
'20161106_172316'
>>> t1 = datetime.datetime.strptime('11/28/2016', "%m/%d/%Y")
datetime.datetime(2016, 11, 28, 0, 0)

>> diff = datetime.datetime.now() - t1
>> diff.days
22 
```
[python datetime format](https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior)
[timedelta](https://docs.python.org/2/library/datetime.html#timedelta-objects)


### I/O

**file path**

```python
    f = r'c:\tmp\test.csv'
    print 'canonical path:', os.path.realpath(__file__)   # c:\tmp\test.csv
    print 'dirname: ', os.path.dirname(os.path.realpath(__file__))  # c:\tmp
    print 'base name: ', os.path.basename(os.path.realpath(__file__))  # test.csv
```

**for each file**

```python
for root, dirs, files in os.walk(d1):
        for n in files:
            print os.path.join(root, n)
```

**find all pdf files**

```python
    for root, dirs, files in os.walk(d1):
        for f in files:
            if f.endswith(".pdf"):
                 print(os.path.join(root, f))
```

**get immediate sub folders**

```python
def get_immediate_subdirectories(root):
    return [d for d in os.listdir(root)
            if os.path.isdir(os.path.join(d, name))]
```

**get human readable file size**

```python
# http://stackoverflow.com/questions/1094841/reusable-library-to-get-human-readable-version-of-file-size
def sizeof_fmt(num, suffix='B'):
    for unit in ['','Ki','Mi','Gi','Ti','Pi','Ei','Zi']:
        if abs(num) < 1024.0:
            return "%3.1f%s%s" % (num, unit, suffix)
        num /= 1024.0
    return "%.1f%s%s" % (num, 'Yi', suffix)
```

**create folder recursively**

```python
os.makedirs(folder-path)
```

**last modified datetime**

```python
last_modified_on = datetime.datetime.fromtimestamp(os.path.getmtime(f))
```

**read/write file**

```python
    with open(file_src) as f:
        lines = f.readlines()

    with open(file_src) as f:
       content = f.read()

    with open(file_dest, mode='w+') as f:
        file_dest.write('content')
```

### Collections 

**map/dict**

```python
users = {'sid1': 'UserA', 'sid2': 'user2'}
for k, v in users.iteritems():
    print k, v
```
**zip**

```python
>>> k=['a', 'b', 'c']
>>> v=[1, 2, 3]
>>> zip(k, v)
[('a', 1), ('b', 2), ('c', 3)]
>>> dict(zip(k, v))
{'a': 1, 'c': 3, 'b': 2}
```

**check if list is a sub-set of another list**
```python
# http://stackoverflow.com/questions/16579085/python-verifying-if-one-list-is-a-subset-of-the-other
set(l1) < set(l2)
```

### XML
```python
from lxml import etree
from lxml import html


if __name__ == '__main__':
    xml = """
    <root>
        <trade>
            <amount>19999</amount>
        </trade>
    </root>
    """

    root = html.fromstring(xml)
    amount = root.xpath('//amount')
    amount[0].text = u'' + str(-1 * int(amount[0].text))

    print etree.tostring(root)

    e_trade_id = root.xpath('/element-not-exists/trade_id')
    if not len(e_trade_id):
        print 'trade_id not found!'

```


## Windows CMD

### String

**find string by keyword "OR"**
```cmd
ipconfig /all | findstr "IPv4 Host"
```
find by 'IPv4' or 'Host'


### Windows OS quick setup

**auto start**
add app shortcut to: 
```
# auto start for all users
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup
# auto start for one user
C:\Users\<user-id>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup  #shorcut: shell:startup
```

### I/O

**robocopy**
```bat
robocopy c:/tmp/sf c:/tmp/dest /MIR

```
return code: `1` - `One of more files were copied successfully.` [robocopy return codes](https://blogs.technet.microsoft.com/deploymentguys/2008/06/16/robocopy-exit-codes/)

**xcopy**
```bat
REM copy folder
xcopy test test-copy2 /f /i /s /e

REM copy file
xcopy mar-18.md mar-18.md-copy*
```

**symbolic link**
```bat
mklink /D ant apache-ant-1.10.1\
symbolic link created for ant <<===>> apache-ant-1.10.1\
```

### Enviroment setup
```bat
setx PATH "C:\dev\tools\ant\bin;%PATH%"
```


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

### Windows Process Port


**find process id by port**
```cmd
netstat -aon | findstr "port1 port2"
```
find by port1 or port2


**find process using port**
```cmd
tasklist /fi "pid eq process-id"
```

### PsExec

### HPC



## Database

### SQL

### H2

### SQL Server / T-SQL

### MySQL



## PowerShell



## Bash

### Linux 
```bash
# show user's groups
groups <user-name>

# add user to group
sudo usermod -a -G <group-name> <user-name>

# log off
logoff
```

## Vim

## Regular Expression

**Python**

```python
s = 'SB20170313AWS123456'
m = re.search('SB\\d{6,8}([a-zA-Z]{3,6})\\d{6}', s)
print m.group(1)
```
**JavaScript**
```javascript
s = 'SB20170313AWS123456'
mc = s.match('SB\\d{6,8}([a-zA-Z]{3,6})\\d{6}')
console.log(mc[1])
```

## IDE

### IntelliJ 

**open file in Explorer:** `ctrl + alt + F12`

**recent files popup** `ctrl + e`

**Maximize editor:** `ctrl + shift + F12`

## C#

### HttpWebRequest with `HTTP Basic Auth`

```csharp
request.Headers.Add("Authorization", String.Concat("Basic ", (Convert.ToBase64String(Encoding.UTF8.GetBytes(string.Format("{0}:", {Your-PrivateKey}))))));
```

## Apache HTTP Server

## .htaccess redirect
```
RewriteEngine on
RewriteBase /
# redirect except /index.html
RewriteCond %{REQUEST_URI} !^/index.html$
RewriteRule ^(.*)$ https://new-demo-website.com/side-projects/$1 [R=301,L]
```

## Java

### execute command line pipes with Runtime.exec()

```java
    public static void main(String[] args) throws IOException {
        Process exec = Runtime.getRuntime().exec("cmd /c ipconfig /all | find \"Host Name\"");

        BufferedReader stdInput = new BufferedReader(new
                InputStreamReader(exec.getInputStream()));

        BufferedReader stdError = new BufferedReader(new
                InputStreamReader(exec.getErrorStream()));

        // read the output from the command
        System.out.println("Here is the standard output of the command:\n");
        String s = null;
        while ((s = stdInput.readLine()) != null) {
            System.out.println(s);
        }

        // read any errors from the attempted command
        System.out.println("Here is the standard error of the command (if any):\n");
        while ((s = stdError.readLine()) != null) {
            System.out.println(s);
        }
    }
```
    
### Maven
  
skipTest:   `mvn install -DskipTests`

### Ant

**build.xml**
```xml
<project name="antExampleProject" default="test" basedir=".">
<target name="test">
    <tstamp/>
    <echo message="today is: ${DSTAMP} - ${TSTAMP} - ${TODAY}" />


    <!-- print all properies -->
    <echoproperties />


    <!-- export property to file -->
    <echo file="host.file" append="false" message='url="github.com"' />


    <!-- load property from file content -->
    <loadresource property="host.file.content">
        <file file="host.file"/>
    </loadresource>
    <echo>file content: ${host.file.content}</echo>


    <!-- execute javascript: extrace value from String -->
    <script language="javascript">
        var s = project.getProperty('host.file.content')
        s = s.substring(s.indexOf('=') + '='.length)
        project.setProperty('host.value', s);
    </script>
    <echo message="host.value found via javascript: ${host.value}" />


    <!-- repalce file content -->
    <replaceregexp file="host.file"
               match='url=\"(.+)\"'
               replace="url.repalced=\1"
               byline="true" />
    <!-- display the file content after refex replace. -->
    <loadresource property="host.replaced">
        <file file="host.file"/>
    </loadresource>
    <echo message="host.replaced: ${host.replaced}" />


    <!-- http get with basic authentication -->
    <get src="https://api.github.com/user" 
        dest="github-user-info.json" username="github-user-login" password="pwd"/>
    <!-- set property from file content -->
    <loadresource property="github.user.info">
        <file file="github-user-info.json"/>
    </loadresource>
    <echo message="user info: ${github.user.info}" />

</target>
</project>
```

## Git

```bash
# print commit log tree
git config --global alias.lgb "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset%n' --abbrev-commit --date=relative --branches"
git lgb
```
[Output of git branch in tree like fashion](http://stackoverflow.com/questions/2421011/output-of-git-branch-in-tree-like-fashion)
